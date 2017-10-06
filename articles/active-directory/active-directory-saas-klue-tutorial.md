---
title: "Tutorial: Integración de Azure Active Directory con Klue | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Klue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="34742-103">Tutorial: Integración de Azure Active Directory con Klue</span><span class="sxs-lookup"><span data-stu-id="34742-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="34742-104">En este tutorial, aprenderá cómo toointegrate Klue con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34742-104">In this tutorial, you learn how toointegrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34742-105">Integración Klue con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="34742-105">Integrating Klue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34742-106">Puede controlar en Azure AD que tenga acceso tooKlue</span><span class="sxs-lookup"><span data-stu-id="34742-106">You can control in Azure AD who has access tooKlue</span></span>
- <span data-ttu-id="34742-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKlue (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34742-107">You can enable your users tooautomatically get signed-on tooKlue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34742-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="34742-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34742-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34742-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34742-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="34742-110">Prerequisites</span></span>

<span data-ttu-id="34742-111">integración de Azure AD con Klue tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="34742-111">tooconfigure Azure AD integration with Klue, you need hello following items:</span></span>

- <span data-ttu-id="34742-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34742-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34742-113">Una suscripción habilitada para el inicio de sesión único en Klue</span><span class="sxs-lookup"><span data-stu-id="34742-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34742-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="34742-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34742-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="34742-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34742-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="34742-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34742-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34742-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34742-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="34742-118">Scenario description</span></span>
<span data-ttu-id="34742-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="34742-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34742-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="34742-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34742-121">Agregar Klue desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="34742-121">Adding Klue from hello gallery</span></span>
2. <span data-ttu-id="34742-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34742-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-hello-gallery"></a><span data-ttu-id="34742-123">Agregar Klue desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="34742-123">Adding Klue from hello gallery</span></span>
<span data-ttu-id="34742-124">integración de hello tooconfigure de Klue en Azure AD, deberá tooadd Klue de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="34742-124">tooconfigure hello integration of Klue into Azure AD, you need tooadd Klue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34742-125">**tooadd Klue de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34742-125">**tooadd Klue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34742-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="34742-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34742-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="34742-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34742-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="34742-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="34742-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34742-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="34742-133">En el cuadro de búsqueda de hello, escriba **Klue**.</span><span class="sxs-lookup"><span data-stu-id="34742-133">In hello search box, type **Klue**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="34742-135">En el panel de resultados de hello, seleccione **Klue**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="34742-135">In hello results panel, select **Klue**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34742-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34742-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34742-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Klue con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="34742-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34742-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Klue es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34742-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Klue is tooa user in Azure AD.</span></span> <span data-ttu-id="34742-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Klue debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="34742-140">In other words, a link relationship between an Azure AD user and hello related user in Klue needs toobe established.</span></span>

<span data-ttu-id="34742-141">En Klue, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="34742-141">In Klue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="34742-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Klue, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="34742-142">tooconfigure and test Azure AD single sign-on with Klue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34742-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="34742-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34742-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34742-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34742-145">**[Crear un usuario de prueba Klue](#creating-a-klue-test-user)**  -toohave un equivalente de Britta Simon en Klue que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="34742-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - toohave a counterpart of Britta Simon in Klue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34742-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="34742-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34742-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="34742-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34742-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34742-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34742-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Klue.</span><span class="sxs-lookup"><span data-stu-id="34742-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="34742-150">**inicio de sesión único en Azure AD tooconfigure con Klue, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34742-150">**tooconfigure Azure AD single sign-on with Klue, perform hello following steps:**</span></span>

1. <span data-ttu-id="34742-151">En el portal de Azure, en Hola Hola **Klue** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="34742-151">In hello Azure portal, on hello **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="34742-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="34742-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="34742-155">En hello **Klue dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="34742-155">On hello **Klue Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="34742-157">a.</span><span class="sxs-lookup"><span data-stu-id="34742-157">a.</span></span> <span data-ttu-id="34742-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="34742-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="34742-159">b.</span><span class="sxs-lookup"><span data-stu-id="34742-159">b.</span></span> <span data-ttu-id="34742-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="34742-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="34742-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="34742-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="34742-162">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="34742-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="34742-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="34742-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="34742-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="34742-165">These values are not real.</span></span> <span data-ttu-id="34742-166">Actualizar estos valores con la dirección URL de respuesta real hello, el identificador y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="34742-166">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="34742-167">Póngase en contacto con [equipo de soporte técnico de cliente de Klue](mailto:support@klue.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="34742-167">Contact [Klue Client support team](mailto:support@klue.com) tooget these values.</span></span>

5. <span data-ttu-id="34742-168">Hola Klue aplicación espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="34742-168">hello Klue application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="34742-169">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="34742-169">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="34742-171">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en hello delante de la imagen y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="34742-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="34742-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="34742-172">Attribute Name</span></span>      | <span data-ttu-id="34742-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="34742-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="34742-174">first_name</span><span class="sxs-lookup"><span data-stu-id="34742-174">first_name</span></span>          | <span data-ttu-id="34742-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="34742-175">user.givenname</span></span> |
    | <span data-ttu-id="34742-176">last_name</span><span class="sxs-lookup"><span data-stu-id="34742-176">last_name</span></span>           | <span data-ttu-id="34742-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="34742-177">user.surname</span></span> |
    | <span data-ttu-id="34742-178">email</span><span class="sxs-lookup"><span data-stu-id="34742-178">email</span></span>               | <span data-ttu-id="34742-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="34742-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="34742-180">a.</span><span class="sxs-lookup"><span data-stu-id="34742-180">a.</span></span> <span data-ttu-id="34742-181">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34742-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="34742-184">b.</span><span class="sxs-lookup"><span data-stu-id="34742-184">b.</span></span> <span data-ttu-id="34742-185">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="34742-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="34742-186">c.</span><span class="sxs-lookup"><span data-stu-id="34742-186">c.</span></span> <span data-ttu-id="34742-187">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="34742-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="34742-188">d.</span><span class="sxs-lookup"><span data-stu-id="34742-188">d.</span></span> <span data-ttu-id="34742-189">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="34742-189">Click **Ok**.</span></span>

7. <span data-ttu-id="34742-190">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="34742-190">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="34742-192">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="34742-192">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="34742-194">En hello **Klue configuración** sección, haga clic en **configurar Klue** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="34742-194">On hello **Klue Configuration** section, click **Configure Klue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="34742-195">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="34742-195">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="34742-197">tooconfigure inicio de sesión único en **Klue** lado, necesita hello toosend descargado **Certificate(Base64) y SAML Single Sign-On dirección URL del servicio, Id. de entidad SAML** demasiado[equipo de soporte técnico de Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="34742-197">tooconfigure single sign-on on **Klue** side, you need toosend hello downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** too[Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="34742-198">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="34742-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34742-199">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="34742-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34742-200">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34742-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34742-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34742-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="34742-202">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="34742-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="34742-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34742-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34742-205">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="34742-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34742-207">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="34742-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34742-209">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="34742-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34742-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="34742-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34742-213">a.</span><span class="sxs-lookup"><span data-stu-id="34742-213">a.</span></span> <span data-ttu-id="34742-214">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34742-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34742-215">b.</span><span class="sxs-lookup"><span data-stu-id="34742-215">b.</span></span> <span data-ttu-id="34742-216">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34742-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34742-217">c.</span><span class="sxs-lookup"><span data-stu-id="34742-217">c.</span></span> <span data-ttu-id="34742-218">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="34742-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34742-219">d.</span><span class="sxs-lookup"><span data-stu-id="34742-219">d.</span></span> <span data-ttu-id="34742-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="34742-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="34742-221">Creación de usuario de prueba de Klue</span><span class="sxs-lookup"><span data-stu-id="34742-221">Creating a Klue test user</span></span>

<span data-ttu-id="34742-222">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Klue toocreate.</span><span class="sxs-lookup"><span data-stu-id="34742-222">hello objective of this section is toocreate a user called Britta Simon in Klue.</span></span> <span data-ttu-id="34742-223">Klue admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="34742-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="34742-224">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="34742-224">There is no action item for you in this section.</span></span> <span data-ttu-id="34742-225">Se crea un nuevo usuario durante un tooaccess intento Klue si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="34742-225">A new user is created during an attempt tooaccess Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="34742-226">Si necesita toocreate manualmente, póngase en contacto con en un usuario [equipo de soporte técnico de Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="34742-226">If you need toocreate a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34742-227">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="34742-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34742-228">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKlue.</span><span class="sxs-lookup"><span data-stu-id="34742-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKlue.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="34742-230">**tooassign Britta Simon tooKlue, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34742-230">**tooassign Britta Simon tooKlue, perform hello following steps:**</span></span>

1. <span data-ttu-id="34742-231">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="34742-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="34742-233">En la lista de aplicaciones de hello, seleccione **Klue**.</span><span class="sxs-lookup"><span data-stu-id="34742-233">In hello applications list, select **Klue**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="34742-235">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="34742-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="34742-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="34742-237">Click **Add** button.</span></span> <span data-ttu-id="34742-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="34742-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="34742-240">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="34742-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34742-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="34742-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34742-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="34742-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34742-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="34742-243">Testing single sign-on</span></span>

<span data-ttu-id="34742-244">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="34742-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="34742-245">Al hacer clic en icono de Klue Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Klue aplicación.</span><span class="sxs-lookup"><span data-stu-id="34742-245">When you click hello Klue tile in hello Access Panel, you should get automatically signed-on tooyour Klue application.</span></span>
<span data-ttu-id="34742-246">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34742-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="34742-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="34742-247">Additional resources</span></span>

* [<span data-ttu-id="34742-248">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34742-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34742-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34742-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

