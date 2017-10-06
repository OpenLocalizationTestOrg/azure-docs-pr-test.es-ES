---
title: "Tutorial: Integración de Azure Active Directory con Lynda.com | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="3850d-103">Tutorial: Integración de Azure Active Directory con Lynda.com</span><span class="sxs-lookup"><span data-stu-id="3850d-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="3850d-104">En este tutorial, aprenderá cómo toointegrate Lynda.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3850d-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3850d-105">Integración de Lynda.com con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3850d-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3850d-106">Puede controlar en Azure AD que tenga acceso tooLynda.com</span><span class="sxs-lookup"><span data-stu-id="3850d-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="3850d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLynda.com (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3850d-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3850d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3850d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3850d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3850d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3850d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3850d-110">Prerequisites</span></span>

<span data-ttu-id="3850d-111">integración de Azure AD con Lynda.com tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3850d-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="3850d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3850d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3850d-113">Una suscripción habilitada para el inicio de sesión único en Lynda.com</span><span class="sxs-lookup"><span data-stu-id="3850d-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3850d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3850d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3850d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3850d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3850d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3850d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3850d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3850d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3850d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3850d-118">Scenario description</span></span>
<span data-ttu-id="3850d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3850d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3850d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3850d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3850d-121">Agregar Lynda.com desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3850d-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="3850d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3850d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="3850d-123">Agregar Lynda.com desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3850d-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="3850d-124">integración de hello tooconfigure de Lynda.com en Azure AD, deberá tooadd Lynda.com de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3850d-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3850d-125">**tooadd Lynda.com desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3850d-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3850d-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3850d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3850d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3850d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3850d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3850d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3850d-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3850d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3850d-133">En el cuadro de búsqueda de hello, escriba **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="3850d-133">In hello search box, type **Lynda.com**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="3850d-135">En el panel de resultados de hello, seleccione **Lynda.com**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3850d-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3850d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3850d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3850d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Lynda.com con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3850d-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3850d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Lynda.com es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3850d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="3850d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Lynda.com debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3850d-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="3850d-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="3850d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="3850d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Lynda.com, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3850d-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3850d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3850d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3850d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3850d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3850d-145">**[Crear un usuario de prueba de Lynda.com](#creating-a-lyndacom-test-user) ** -toohave un equivalente de Britta Simon en Lynda.com que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3850d-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3850d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3850d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3850d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3850d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3850d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3850d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3850d-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="3850d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="3850d-150">**inicio de sesión único en tooconfigure Azure AD con Lynda.com, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3850d-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="3850d-151">En el portal de Azure, en Hola Hola **Lynda.com** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3850d-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3850d-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3850d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="3850d-155">En hello **Lynda.com dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3850d-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="3850d-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="3850d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3850d-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="3850d-158">This value is not real.</span></span> <span data-ttu-id="3850d-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="3850d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3850d-160">Póngase en contacto con [equipo de soporte técnico de Lynda.com cliente](https://www.linkedin.com/help/lynda/ask) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="3850d-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="3850d-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3850d-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="3850d-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3850d-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3850d-165">tooconfigure inicio de sesión único en **Lynda.com** lado, necesita hello toosend descargado **Metadata XML** [soporte técnico de Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="3850d-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3850d-166">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3850d-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="3850d-167">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3850d-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3850d-169">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3850d-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3850d-170">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3850d-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3850d-172">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3850d-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3850d-174">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3850d-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3850d-176">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3850d-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3850d-178">a.</span><span class="sxs-lookup"><span data-stu-id="3850d-178">a.</span></span> <span data-ttu-id="3850d-179">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3850d-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3850d-180">b.</span><span class="sxs-lookup"><span data-stu-id="3850d-180">b.</span></span> <span data-ttu-id="3850d-181">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3850d-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3850d-182">c.</span><span class="sxs-lookup"><span data-stu-id="3850d-182">c.</span></span> <span data-ttu-id="3850d-183">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3850d-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3850d-184">d.</span><span class="sxs-lookup"><span data-stu-id="3850d-184">d.</span></span> <span data-ttu-id="3850d-185">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3850d-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="3850d-186">Creación de un usuario de prueba de Lynda.com</span><span class="sxs-lookup"><span data-stu-id="3850d-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="3850d-187">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="3850d-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="3850d-188">Cuando un usuario asignado intenta toolog en tooLynda.com mediante el panel de acceso de hello, Lynda.com comprueba si existe el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3850d-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="3850d-189">Si no hay cuentas de usuario disponibles, Lynda.com crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3850d-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="3850d-190">Puede usar cualquier otra Lynda.com usuario cuenta herramienta de creación o las API proporcionadas por Lynda.com tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="3850d-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3850d-191">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3850d-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3850d-192">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="3850d-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3850d-194">**tooassign Britta Simon tooLynda.com, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3850d-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="3850d-195">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3850d-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3850d-197">En la lista de aplicaciones de hello, seleccione **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="3850d-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="3850d-199">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3850d-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3850d-201">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3850d-201">Click **Add** button.</span></span> <span data-ttu-id="3850d-202">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3850d-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3850d-204">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3850d-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3850d-205">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3850d-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3850d-206">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3850d-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3850d-207">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3850d-207">Testing single sign-on</span></span>

<span data-ttu-id="3850d-208">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3850d-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="3850d-209">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3850d-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3850d-210">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3850d-210">Additional resources</span></span>

* [<span data-ttu-id="3850d-211">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3850d-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3850d-212">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3850d-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

