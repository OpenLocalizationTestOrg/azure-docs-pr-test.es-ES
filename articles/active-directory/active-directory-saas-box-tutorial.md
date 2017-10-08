---
title: "Tutorial: Integración de Azure Active Directory con Box | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="80a6f-103">Tutorial: Integración de Azure Active Directory con Box</span><span class="sxs-lookup"><span data-stu-id="80a6f-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="80a6f-104">En este tutorial, aprenderá cómo toointegrate cuadro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80a6f-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80a6f-105">Cuadro de la integración con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="80a6f-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80a6f-106">Puede controlar en Azure AD con el cuadro de herramientas de acceso</span><span class="sxs-lookup"><span data-stu-id="80a6f-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="80a6f-107">Puede habilitar los usuarios tooautomatically get firmado en cuadro de herramientas (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a6f-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80a6f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="80a6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="80a6f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80a6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80a6f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="80a6f-110">Prerequisites</span></span>

<span data-ttu-id="80a6f-111">integración de Azure AD con Box tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="80a6f-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="80a6f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80a6f-113">Una suscripción a Box habilitada para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="80a6f-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80a6f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="80a6f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80a6f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="80a6f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80a6f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="80a6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80a6f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80a6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80a6f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="80a6f-118">Scenario description</span></span>
<span data-ttu-id="80a6f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="80a6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80a6f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="80a6f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80a6f-121">Agregar cuadro de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="80a6f-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="80a6f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="80a6f-123">Agregar cuadro de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="80a6f-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="80a6f-124">integración de hello tooconfigure del cuadro en Azure AD, deberá tooadd cuadro de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="80a6f-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80a6f-125">**tooadd cuadro desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80a6f-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a6f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="80a6f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80a6f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80a6f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="80a6f-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="80a6f-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="80a6f-133">En el cuadro de búsqueda de hello, escriba **cuadro**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-133">In hello search box, type **Box**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="80a6f-135">En el panel de resultados de hello, seleccione **cuadro**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="80a6f-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80a6f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80a6f-138">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con Box con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="80a6f-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="80a6f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en cuadro es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80a6f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="80a6f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en cuadro debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="80a6f-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="80a6f-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="80a6f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="80a6f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con cuadro, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="80a6f-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80a6f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="80a6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80a6f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80a6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80a6f-145">**[Crear un usuario de prueba cuadro](#creating-a-box-test-user)**  -toohave un equivalente de Britta Simon en el cuadro que tenga representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="80a6f-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80a6f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="80a6f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80a6f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="80a6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80a6f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80a6f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de cuadro.</span><span class="sxs-lookup"><span data-stu-id="80a6f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="80a6f-150">**inicio de sesión único en tooconfigure Azure AD con cuadro, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80a6f-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a6f-151">En el portal de Azure, en Hola Hola **cuadro** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="80a6f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="80a6f-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="80a6f-155">En hello **cuadro dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="80a6f-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="80a6f-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="80a6f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="80a6f-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="80a6f-158">This value is not real.</span></span> <span data-ttu-id="80a6f-159">Actualice el valor de hello con URL de inicio de sesión real de Hola.</span><span class="sxs-lookup"><span data-stu-id="80a6f-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="80a6f-160">Póngase en contacto con [equipo de soporte técnico de cliente cuadro](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="80a6f-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="80a6f-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="80a6f-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="80a6f-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="80a6f-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="80a6f-165">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de cliente cuadro](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) y proporcionarles Hola Descargar archivo XML.</span><span class="sxs-lookup"><span data-stu-id="80a6f-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="80a6f-166">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="80a6f-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80a6f-167">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="80a6f-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80a6f-168">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80a6f-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80a6f-169">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a6f-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="80a6f-170">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="80a6f-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="80a6f-172">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80a6f-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a6f-173">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="80a6f-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80a6f-175">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80a6f-177">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="80a6f-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80a6f-179">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="80a6f-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80a6f-181">a.</span><span class="sxs-lookup"><span data-stu-id="80a6f-181">a.</span></span> <span data-ttu-id="80a6f-182">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80a6f-183">b.</span><span class="sxs-lookup"><span data-stu-id="80a6f-183">b.</span></span> <span data-ttu-id="80a6f-184">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="80a6f-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80a6f-185">c.</span><span class="sxs-lookup"><span data-stu-id="80a6f-185">c.</span></span> <span data-ttu-id="80a6f-186">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="80a6f-187">d.</span><span class="sxs-lookup"><span data-stu-id="80a6f-187">d.</span></span> <span data-ttu-id="80a6f-188">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="80a6f-189">Creación de usuario de prueba de Box</span><span class="sxs-lookup"><span data-stu-id="80a6f-189">Creating a Box test user</span></span>

<span data-ttu-id="80a6f-190">En esta sección, se crea un usuario llamado a Britta Simon en Box.</span><span class="sxs-lookup"><span data-stu-id="80a6f-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="80a6f-191">Box admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="80a6f-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="80a6f-192">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="80a6f-192">There is no action item for you in this section.</span></span> <span data-ttu-id="80a6f-193">Si un usuario ya no existe en el cuadro, se crea uno nuevo si intentas tooaccess cuadro.</span><span class="sxs-lookup"><span data-stu-id="80a6f-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="80a6f-194">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a6f-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="80a6f-195">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de cuadro de herramientas de acceso.</span><span class="sxs-lookup"><span data-stu-id="80a6f-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="80a6f-197">**tooassign Britta Simon de cuadro de herramientas, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80a6f-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a6f-198">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="80a6f-200">En la lista de aplicaciones de hello, seleccione **cuadro**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-200">In hello applications list, select **Box**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="80a6f-202">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="80a6f-204">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-204">Click **Add** button.</span></span> <span data-ttu-id="80a6f-205">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="80a6f-207">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="80a6f-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80a6f-208">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80a6f-209">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80a6f-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80a6f-210">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="80a6f-210">Testing single sign-on</span></span>

<span data-ttu-id="80a6f-211">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="80a6f-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80a6f-212">Al hacer clic en icono de cuadro de Hola Hola Panel de acceso, deberá obtener inicio de sesión página tooget ha iniciado sesión tooyour aplicación estándar.</span><span class="sxs-lookup"><span data-stu-id="80a6f-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80a6f-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="80a6f-213">Additional resources</span></span>

* [<span data-ttu-id="80a6f-214">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80a6f-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80a6f-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80a6f-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="80a6f-216">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="80a6f-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

