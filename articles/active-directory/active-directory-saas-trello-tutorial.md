---
title: "Tutorial: integración de Azure Active Directory con Trello | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="de41a-103">Tutorial: integración de Azure Active Directory con Trello</span><span class="sxs-lookup"><span data-stu-id="de41a-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="de41a-104">En este tutorial, aprenderá cómo toointegrate Trello con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de41a-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de41a-105">Integración Trello con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="de41a-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de41a-106">Puede controlar en Azure AD que tenga acceso tooTrello</span><span class="sxs-lookup"><span data-stu-id="de41a-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="de41a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTrello (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de41a-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de41a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="de41a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de41a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de41a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de41a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="de41a-110">Prerequisites</span></span>

<span data-ttu-id="de41a-111">integración de Azure AD con Trello tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="de41a-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="de41a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de41a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de41a-113">Una suscripción habilitada para inicio de sesión único en Trello</span><span class="sxs-lookup"><span data-stu-id="de41a-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de41a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="de41a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de41a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="de41a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de41a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="de41a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de41a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de41a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de41a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="de41a-118">Scenario description</span></span>
<span data-ttu-id="de41a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="de41a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de41a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="de41a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de41a-121">Agregar Trello desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="de41a-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="de41a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de41a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="de41a-123">Agregar Trello desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="de41a-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="de41a-124">integración de hello tooconfigure de Trello en Azure AD, deberá tooadd Trello de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="de41a-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de41a-125">**tooadd Trello de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="de41a-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de41a-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="de41a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de41a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="de41a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de41a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="de41a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="de41a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="de41a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="de41a-133">En el cuadro de búsqueda de hello, escriba **Trello**.</span><span class="sxs-lookup"><span data-stu-id="de41a-133">In hello search box, type **Trello**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="de41a-135">En el panel de resultados de hello, seleccione **Trello**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="de41a-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de41a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de41a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de41a-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Trello con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="de41a-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de41a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Trello es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de41a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="de41a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Trello debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="de41a-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="de41a-141">En Trello, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="de41a-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="de41a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Trello, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="de41a-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de41a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="de41a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de41a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de41a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de41a-145">**[Crear un usuario de prueba Trello](#creating-a-trello-test-user) ** -toohave un equivalente de Britta Simon en Trello que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="de41a-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de41a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="de41a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de41a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="de41a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de41a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de41a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de41a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Trello.</span><span class="sxs-lookup"><span data-stu-id="de41a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="de41a-150">**inicio de sesión único en Azure AD tooconfigure con Trello, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="de41a-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="de41a-151">En el portal de Azure, en Hola Hola **Trello** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="de41a-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="de41a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="de41a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="de41a-155">En hello **Trello dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="de41a-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="de41a-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="de41a-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="de41a-158">En hello **Trello dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="de41a-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="de41a-160">a.</span><span class="sxs-lookup"><span data-stu-id="de41a-160">a.</span></span> <span data-ttu-id="de41a-161">Haga clic en hello **mostrar avanzadas de configuración de la URL**.</span><span class="sxs-lookup"><span data-stu-id="de41a-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="de41a-162">b.</span><span class="sxs-lookup"><span data-stu-id="de41a-162">b.</span></span> <span data-ttu-id="de41a-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="de41a-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="de41a-164">Debe obtener hello ** \<enterprise\> ** slug de Trello.</span><span class="sxs-lookup"><span data-stu-id="de41a-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="de41a-165">Si no tiene valor slug de hello, póngase en contacto con [equipo de soporte técnico de Trello](mailto:support@trello.com) tooget slug de hello para empresas.</span><span class="sxs-lookup"><span data-stu-id="de41a-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="de41a-166">Aplicación de Trello espera atributos específicos del toocontain de aserciones SAML Hola.</span><span class="sxs-lookup"><span data-stu-id="de41a-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="de41a-167">Configurar Hola siguientes atributos para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="de41a-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="de41a-168">Puede administrar valores de hello de estos atributos de hello **"Atributos de usuario"** de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="de41a-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="de41a-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="de41a-169">hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="de41a-171">En hello **atributos de token SAML** cuadro de diálogo, para cada fila se muestra en la tabla de Hola a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="de41a-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="de41a-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="de41a-172">Attribute Name</span></span> | <span data-ttu-id="de41a-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="de41a-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="de41a-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="de41a-174">User.Email</span></span> | <span data-ttu-id="de41a-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="de41a-175">user.mail</span></span> |
    | <span data-ttu-id="de41a-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="de41a-176">User.FirstName</span></span> | <span data-ttu-id="de41a-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="de41a-177">user.givenname</span></span> |
    | <span data-ttu-id="de41a-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="de41a-178">User.LastName</span></span> | <span data-ttu-id="de41a-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="de41a-179">user.surname</span></span> |

    <span data-ttu-id="de41a-180">a.</span><span class="sxs-lookup"><span data-stu-id="de41a-180">a.</span></span> <span data-ttu-id="de41a-181">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="de41a-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="de41a-184">b.</span><span class="sxs-lookup"><span data-stu-id="de41a-184">b.</span></span> <span data-ttu-id="de41a-185">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="de41a-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="de41a-186">c.</span><span class="sxs-lookup"><span data-stu-id="de41a-186">c.</span></span> <span data-ttu-id="de41a-187">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="de41a-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="de41a-188">d.</span><span class="sxs-lookup"><span data-stu-id="de41a-188">d.</span></span> <span data-ttu-id="de41a-189">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="de41a-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="de41a-190">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="de41a-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="de41a-192">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="de41a-192">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de41a-194">En hello **Trello configuración** sección, haga clic en **configurar Trello** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="de41a-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="de41a-195">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="de41a-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="de41a-197">tooget SSO configurado para la aplicación, vaya demasiado[configuración de SSO empresarial Trello](https://trello.com/sso-configuration) página toosend [equipo de soporte técnico de Trello](mailto:support@trello.com) hello **SAML Single Sign-On dirección URL del servicio** y adjuntar hello **certificado (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="de41a-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="de41a-198">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="de41a-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de41a-199">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="de41a-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de41a-200">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de41a-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de41a-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de41a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="de41a-202">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="de41a-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="de41a-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="de41a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de41a-205">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="de41a-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de41a-207">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="de41a-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de41a-209">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="de41a-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de41a-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="de41a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de41a-213">a.</span><span class="sxs-lookup"><span data-stu-id="de41a-213">a.</span></span> <span data-ttu-id="de41a-214">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de41a-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de41a-215">b.</span><span class="sxs-lookup"><span data-stu-id="de41a-215">b.</span></span> <span data-ttu-id="de41a-216">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="de41a-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de41a-217">c.</span><span class="sxs-lookup"><span data-stu-id="de41a-217">c.</span></span> <span data-ttu-id="de41a-218">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="de41a-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de41a-219">d.</span><span class="sxs-lookup"><span data-stu-id="de41a-219">d.</span></span> <span data-ttu-id="de41a-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="de41a-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="de41a-221">Creación de usuario de prueba de Trello</span><span class="sxs-lookup"><span data-stu-id="de41a-221">Creating a Trello test user</span></span>

<span data-ttu-id="de41a-222">En esta sección, creará un usuario llamado Britta Simon en Trello.</span><span class="sxs-lookup"><span data-stu-id="de41a-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="de41a-223">En esta sección, creará un usuario llamado Britta Simon en Trello.</span><span class="sxs-lookup"><span data-stu-id="de41a-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="de41a-224">Trello admite el aprovisionamiento de just-in-time y crea una nueva cuenta es Hola primera vez que inicie sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de41a-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de41a-225">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="de41a-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de41a-226">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTrello.</span><span class="sxs-lookup"><span data-stu-id="de41a-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="de41a-228">**tooassign Britta Simon tooTrello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="de41a-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="de41a-229">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="de41a-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="de41a-231">En la lista de aplicaciones de hello, seleccione **Trello**.</span><span class="sxs-lookup"><span data-stu-id="de41a-231">In hello applications list, select **Trello**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="de41a-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="de41a-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="de41a-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="de41a-235">Click **Add** button.</span></span> <span data-ttu-id="de41a-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="de41a-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="de41a-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="de41a-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de41a-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="de41a-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de41a-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="de41a-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de41a-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="de41a-241">Testing single sign-on</span></span>

<span data-ttu-id="de41a-242">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="de41a-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="de41a-243">Al hacer clic en icono de Trello Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Trello aplicación.</span><span class="sxs-lookup"><span data-stu-id="de41a-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de41a-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="de41a-244">Additional resources</span></span>

* [<span data-ttu-id="de41a-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de41a-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de41a-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de41a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

