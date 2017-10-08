---
title: "Tutorial: Integración de Azure Active Directory con Inkling | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="c1574-103">Tutorial: Integración de Azure Active Directory con Inkling</span><span class="sxs-lookup"><span data-stu-id="c1574-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="c1574-104">En este tutorial, aprenderá cómo toointegrate Inkling con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1574-104">In this tutorial, you learn how toointegrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1574-105">Integración Inkling con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c1574-105">Integrating Inkling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c1574-106">Puede controlar en Azure AD que tenga acceso tooInkling</span><span class="sxs-lookup"><span data-stu-id="c1574-106">You can control in Azure AD who has access tooInkling</span></span>
- <span data-ttu-id="c1574-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooInkling (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1574-107">You can enable your users tooautomatically get signed-on tooInkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1574-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="c1574-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="c1574-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1574-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1574-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c1574-110">Prerequisites</span></span>

<span data-ttu-id="c1574-111">integración de Azure AD con Inkling tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c1574-111">tooconfigure Azure AD integration with Inkling, you need hello following items:</span></span>

- <span data-ttu-id="c1574-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1574-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1574-113">Una suscripción habilitada para inicio de sesión único en Inkling</span><span class="sxs-lookup"><span data-stu-id="c1574-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="c1574-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c1574-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c1574-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c1574-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1574-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c1574-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c1574-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1574-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c1574-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c1574-118">Scenario description</span></span>
<span data-ttu-id="c1574-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c1574-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1574-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c1574-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1574-121">Agregar Inkling desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c1574-121">Adding Inkling from hello gallery</span></span>
2. <span data-ttu-id="c1574-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1574-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-hello-gallery"></a><span data-ttu-id="c1574-123">Agregar Inkling desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c1574-123">Adding Inkling from hello gallery</span></span>
<span data-ttu-id="c1574-124">integración de hello tooconfigure de Inkling en Azure AD, deberá tooadd Inkling de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c1574-124">tooconfigure hello integration of Inkling into Azure AD, you need tooadd Inkling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c1574-125">**tooadd Inkling de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c1574-125">**tooadd Inkling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1574-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c1574-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1574-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c1574-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c1574-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c1574-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c1574-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1574-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c1574-133">En el cuadro de búsqueda de hello, escriba **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="c1574-133">In hello search box, type **Inkling**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="c1574-135">En el panel de resultados de hello, seleccione **Inkling**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c1574-135">In hello results panel, select **Inkling**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1574-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1574-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1574-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Inkling con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1574-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1574-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Inkling es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1574-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Inkling is tooa user in Azure AD.</span></span> <span data-ttu-id="c1574-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Inkling debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c1574-140">In other words, a link relationship between an Azure AD user and hello related user in Inkling needs toobe established.</span></span>

<span data-ttu-id="c1574-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Inkling.</span><span class="sxs-lookup"><span data-stu-id="c1574-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Inkling.</span></span>

<span data-ttu-id="c1574-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Inkling, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c1574-142">tooconfigure and test Azure AD single sign-on with Inkling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c1574-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c1574-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c1574-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1574-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1574-145">**[Creación de un usuario de prueba Inkling](#creating-an-inkling-test-user)**  -toohave un equivalente de Britta Simon en Inkling que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="c1574-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - toohave a counterpart of Britta Simon in Inkling that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c1574-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c1574-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1574-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c1574-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1574-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1574-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1574-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Inkling.</span><span class="sxs-lookup"><span data-stu-id="c1574-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="c1574-150">**inicio de sesión único en Azure AD tooconfigure con Inkling, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c1574-150">**tooconfigure Azure AD single sign-on with Inkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1574-151">En el portal de administración de Azure de hello, en hello **Inkling** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c1574-151">In hello Azure Management portal, on hello **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c1574-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c1574-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="c1574-155">En hello **Inkling dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c1574-155">On hello **Inkling Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="c1574-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1574-157">a.</span></span> <span data-ttu-id="c1574-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="c1574-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="c1574-159">b.</span><span class="sxs-lookup"><span data-stu-id="c1574-159">b.</span></span> <span data-ttu-id="c1574-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="c1574-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1574-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1574-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="c1574-162">Tener tooupdate estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="c1574-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c1574-163">Póngase en contacto con [equipo de soporte técnico de Inkling](mailto:press@inkling.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="c1574-163">Contact [Inkling support team](mailto:press@inkling.com) tooget these values.</span></span>

4. <span data-ttu-id="c1574-164">En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="c1574-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="c1574-166">En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="c1574-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="c1574-167">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c1574-167">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="c1574-169">En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="c1574-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="c1574-171">En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c1574-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="c1574-173">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c1574-173">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="c1574-175">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de Inkling](mailto:press@inkling.com) y proporcióneles con descargado **metadatos**.</span><span class="sxs-lookup"><span data-stu-id="c1574-175">tooget SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1574-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1574-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1574-177">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c1574-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c1574-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c1574-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1574-180">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c1574-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1574-182">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c1574-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1574-184">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1574-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1574-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c1574-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1574-188">a.</span><span class="sxs-lookup"><span data-stu-id="c1574-188">a.</span></span> <span data-ttu-id="c1574-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1574-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1574-190">b.</span><span class="sxs-lookup"><span data-stu-id="c1574-190">b.</span></span> <span data-ttu-id="c1574-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c1574-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1574-192">c.</span><span class="sxs-lookup"><span data-stu-id="c1574-192">c.</span></span> <span data-ttu-id="c1574-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c1574-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c1574-194">d.</span><span class="sxs-lookup"><span data-stu-id="c1574-194">d.</span></span> <span data-ttu-id="c1574-195">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="c1574-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="c1574-196">Creación de un usuario de prueba de Inkling</span><span class="sxs-lookup"><span data-stu-id="c1574-196">Creating an Inkling test user</span></span>

<span data-ttu-id="c1574-197">En esta sección, creará un usuario llamado Britta Simon en Inkling.</span><span class="sxs-lookup"><span data-stu-id="c1574-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="c1574-198">Trabaje con [equipo de soporte técnico de Inkling](mailto:press@inkling.com) a los usuarios de tooadd hello en la plataforma de Inkling Hola.</span><span class="sxs-lookup"><span data-stu-id="c1574-198">Please work with [Inkling support team](mailto:press@inkling.com) tooadd hello users in hello Inkling platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c1574-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1574-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c1574-200">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooInkling de acceso.</span><span class="sxs-lookup"><span data-stu-id="c1574-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooInkling.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c1574-202">**tooassign Britta Simon tooInkling, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c1574-202">**tooassign Britta Simon tooInkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1574-203">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c1574-203">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c1574-205">En la lista de aplicaciones de hello, seleccione **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="c1574-205">In hello applications list, select **Inkling**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="c1574-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c1574-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c1574-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c1574-209">Click **Add** button.</span></span> <span data-ttu-id="c1574-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c1574-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c1574-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1574-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c1574-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c1574-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1574-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c1574-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="c1574-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c1574-215">Testing single sign-on</span></span>

<span data-ttu-id="c1574-216">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c1574-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c1574-217">Al hacer clic en icono de Inkling Hola Hola Panel de acceso, deberá obtener la aplicación de Inkling tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="c1574-217">When you click hello Inkling tile in hello Access Panel, you should get automatically signed-on tooyour Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c1574-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c1574-218">Additional resources</span></span>

* [<span data-ttu-id="c1574-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1574-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1574-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1574-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png