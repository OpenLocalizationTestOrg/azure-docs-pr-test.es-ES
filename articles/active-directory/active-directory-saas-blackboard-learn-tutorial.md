---
title: "Tutorial: Integración de Azure Active Directory con Blackboard Learn | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y obtenga información acerca de Pizarra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="bad2b-103">Tutorial: Integración de Azure Active Directory con Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="bad2b-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="bad2b-104">En este tutorial, aprenderá cómo toointegrate Pizarra aprender con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bad2b-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bad2b-105">Pizarra obtener información sobre la integración con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bad2b-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bad2b-106">Puede controlar en Azure AD que tenga acceso tooBlackboard más información</span><span class="sxs-lookup"><span data-stu-id="bad2b-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="bad2b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBlackboard más información (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bad2b-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bad2b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bad2b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bad2b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bad2b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bad2b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bad2b-110">Prerequisites</span></span>

<span data-ttu-id="bad2b-111">tooconfigure integración de Azure AD con pizarra aprender, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bad2b-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="bad2b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bad2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bad2b-113">Una suscripción habilitada para el inicio de sesión único de Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="bad2b-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bad2b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bad2b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bad2b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bad2b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bad2b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bad2b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bad2b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bad2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bad2b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bad2b-118">Scenario description</span></span>
<span data-ttu-id="bad2b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bad2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bad2b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bad2b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bad2b-121">Agregar Pizarra Obtenga información acerca de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bad2b-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="bad2b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bad2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="bad2b-123">Agregar Pizarra Obtenga información acerca de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bad2b-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="bad2b-124">integración de hello tooconfigure de aprender Pizarra en Azure AD, deberá tooadd Pizarra Obtenga información acerca de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bad2b-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bad2b-125">**tooadd Pizarra aprender de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bad2b-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bad2b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bad2b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bad2b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bad2b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bad2b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bad2b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bad2b-133">En el cuadro de búsqueda de hello, escriba **Pizarra aprender**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="bad2b-135">En el panel de resultados de hello, seleccione **Pizarra aprender**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bad2b-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bad2b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bad2b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bad2b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Blackboard Learn con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bad2b-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bad2b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en aprender Pizarra es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bad2b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="bad2b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en aprender Pizarra debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="bad2b-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="bad2b-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en aprender Pizarra.</span><span class="sxs-lookup"><span data-stu-id="bad2b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="bad2b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con pizarra aprender, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bad2b-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bad2b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="bad2b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bad2b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bad2b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bad2b-145">**[Crear un usuario de prueba Pizarra aprender](#creating-a-blackboard-learn-test-user)**  -toohave un equivalente de Britta Simon en pizarra obtener información que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="bad2b-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bad2b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bad2b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bad2b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bad2b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bad2b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bad2b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bad2b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación obtenga información acerca de Pizarra.</span><span class="sxs-lookup"><span data-stu-id="bad2b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="bad2b-150">**inicio de sesión único en tooconfigure Azure AD con obtener Pizarra, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bad2b-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="bad2b-151">En el portal de Azure, en Hola Hola **Pizarra aprender** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bad2b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bad2b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="bad2b-155">En hello **Pizarra Obtenga información acerca de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bad2b-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="bad2b-157">a.</span><span class="sxs-lookup"><span data-stu-id="bad2b-157">a.</span></span> <span data-ttu-id="bad2b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="bad2b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="bad2b-159">b.</span><span class="sxs-lookup"><span data-stu-id="bad2b-159">b.</span></span> <span data-ttu-id="bad2b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="bad2b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="bad2b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="bad2b-161">These values are not real.</span></span> <span data-ttu-id="bad2b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="bad2b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bad2b-163">Póngase en contacto con [equipo de soporte técnico de cliente obtenga información acerca de pizarra](https://www.blackboard.com/support/index.aspx) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="bad2b-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="bad2b-164">Aplicación de aprendizaje de pizarra espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="bad2b-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="bad2b-165">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="bad2b-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="bad2b-166">Puede administrar valores de hello de estos atributos de hello **atributos de usuario** sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bad2b-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="bad2b-167">Hola siguiente captura de pantalla muestra un ejemplo sobre él.</span><span class="sxs-lookup"><span data-stu-id="bad2b-167">hello following screenshot shows an example about it.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="bad2b-169">Hola **atributos de usuario** sección **inicio de sesión único** cuadro de diálogo, configurar atributos de token SAML, tal y como se muestra en la imagen de Hola y realizar pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bad2b-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="bad2b-170">Hemos asignamos Hola Userprincipalname como atributo de usuario único Hola aquí pero se puede asignar toohello valor adecuado, que distingue de forma única usuario Hola de organización de Hola y que asigna el campo de nombre de usuario de tooBlackboard más información.</span><span class="sxs-lookup"><span data-stu-id="bad2b-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="bad2b-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="bad2b-171">Attribute Name</span></span> | <span data-ttu-id="bad2b-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="bad2b-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="bad2b-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="bad2b-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="bad2b-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="bad2b-174">user.userprincipalname</span></span> |

    <span data-ttu-id="bad2b-175">a.</span><span class="sxs-lookup"><span data-stu-id="bad2b-175">a.</span></span> <span data-ttu-id="bad2b-176">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bad2b-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bad2b-179">b.</span><span class="sxs-lookup"><span data-stu-id="bad2b-179">b.</span></span> <span data-ttu-id="bad2b-180">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="bad2b-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="bad2b-181">c.</span><span class="sxs-lookup"><span data-stu-id="bad2b-181">c.</span></span> <span data-ttu-id="bad2b-182">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="bad2b-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bad2b-183">d.</span><span class="sxs-lookup"><span data-stu-id="bad2b-183">d.</span></span> <span data-ttu-id="bad2b-184">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-184">Click **Ok**.</span></span>

4. <span data-ttu-id="bad2b-185">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bad2b-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="bad2b-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bad2b-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bad2b-189">En hello **Pizarra obtener información sobre configuración** sección, haga clic en **configurar Obtenga información acerca de pizarra** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="bad2b-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bad2b-190">Hola copia **Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="bad2b-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="bad2b-192">tooconfigure inicio de sesión único en **Pizarra Obtenga información** lado, necesita hello toosend descargado **Metadata XML** y **Id. de entidad SAML** demasiado[Obtenga información acerca de Pizarra admitir](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="bad2b-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="bad2b-193">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="bad2b-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bad2b-194">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="bad2b-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bad2b-195">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bad2b-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bad2b-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bad2b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="bad2b-197">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bad2b-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bad2b-199">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bad2b-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bad2b-200">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bad2b-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bad2b-202">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bad2b-204">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bad2b-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bad2b-206">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bad2b-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bad2b-208">a.</span><span class="sxs-lookup"><span data-stu-id="bad2b-208">a.</span></span> <span data-ttu-id="bad2b-209">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bad2b-210">b.</span><span class="sxs-lookup"><span data-stu-id="bad2b-210">b.</span></span> <span data-ttu-id="bad2b-211">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bad2b-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bad2b-212">c.</span><span class="sxs-lookup"><span data-stu-id="bad2b-212">c.</span></span> <span data-ttu-id="bad2b-213">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bad2b-214">d.</span><span class="sxs-lookup"><span data-stu-id="bad2b-214">d.</span></span> <span data-ttu-id="bad2b-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="bad2b-216">Creación de un usuario de prueba de Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="bad2b-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="bad2b-217">En esta sección, creará un usuario llamado Britta Simon en Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="bad2b-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="bad2b-218">Compatibilidad de aplicaciones de Blackboard Learn para el aprovisionamiento de usuarios justo a tiempo.</span><span class="sxs-lookup"><span data-stu-id="bad2b-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="bad2b-219">Asegúrese de que ha configurado notificaciones Hola tal y como se describe en la sección de hello  **[configurar Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="bad2b-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bad2b-220">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bad2b-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bad2b-221">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBlackboard más información.</span><span class="sxs-lookup"><span data-stu-id="bad2b-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bad2b-223">**tooassign Britta Simon tooBlackboard más información, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bad2b-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="bad2b-224">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bad2b-226">En la lista de aplicaciones de hello, seleccione **Pizarra aprender**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="bad2b-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bad2b-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-230">Click **Add** button.</span></span> <span data-ttu-id="bad2b-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bad2b-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bad2b-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bad2b-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bad2b-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bad2b-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bad2b-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bad2b-236">Testing single sign-on</span></span>

<span data-ttu-id="bad2b-237">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bad2b-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bad2b-238">Al hacer clic en icono Pizarra Obtenga información acerca de Hola Hola Panel de acceso, deberá obtener la aplicación Pizarra Obtenga información acerca de tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="bad2b-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="bad2b-239">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bad2b-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bad2b-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bad2b-240">Additional resources</span></span>

* [<span data-ttu-id="bad2b-241">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bad2b-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bad2b-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bad2b-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

