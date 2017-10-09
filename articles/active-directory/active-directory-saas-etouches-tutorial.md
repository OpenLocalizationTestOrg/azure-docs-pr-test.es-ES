---
title: "Tutorial: Integración de Azure Active Directory con etouches | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="340f1-103">Tutorial: Integración de Azure Active Directory con etouches</span><span class="sxs-lookup"><span data-stu-id="340f1-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="340f1-104">En este tutorial, aprenderá cómo toointegrate etouches con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="340f1-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="340f1-105">Integración etouches con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="340f1-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="340f1-106">Puede controlar en Azure AD que tenga acceso tooetouches</span><span class="sxs-lookup"><span data-stu-id="340f1-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="340f1-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooetouches (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="340f1-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="340f1-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="340f1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="340f1-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="340f1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="340f1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="340f1-110">Prerequisites</span></span>

<span data-ttu-id="340f1-111">integración de Azure AD con etouches tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="340f1-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="340f1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="340f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="340f1-113">Una suscripción habilitada para el inicio de sesión único en etouches</span><span class="sxs-lookup"><span data-stu-id="340f1-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="340f1-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="340f1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="340f1-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="340f1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="340f1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="340f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="340f1-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="340f1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="340f1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="340f1-118">Scenario description</span></span>
<span data-ttu-id="340f1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="340f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="340f1-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="340f1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="340f1-121">Agregar etouches desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="340f1-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="340f1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="340f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="340f1-123">Agregar etouches desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="340f1-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="340f1-124">integración de hello tooconfigure de etouches en Azure AD, deberá tooadd etouches de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="340f1-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="340f1-125">**tooadd etouches de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="340f1-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="340f1-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="340f1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="340f1-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="340f1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="340f1-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="340f1-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="340f1-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="340f1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="340f1-133">En el cuadro de búsqueda de hello, escriba **etouches**, seleccione **etouches** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="340f1-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![etouches en la lista de resultados de Hola](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="340f1-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="340f1-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="340f1-136">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con etouches con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="340f1-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="340f1-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en etouches es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="340f1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="340f1-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en etouches debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="340f1-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="340f1-139">En etouches, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="340f1-140">tooconfigure y prueba de inicio de sesión único en Azure AD con etouches, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="340f1-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="340f1-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="340f1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="340f1-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="340f1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="340f1-143">**[Crear un usuario de prueba etouches](#create-an-etouches-test-user)**  -toohave un equivalente de Britta Simon en etouches que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="340f1-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="340f1-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="340f1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="340f1-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="340f1-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="340f1-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="340f1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="340f1-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación etouches.</span><span class="sxs-lookup"><span data-stu-id="340f1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="340f1-148">**inicio de sesión único en Azure AD tooconfigure con etouches, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="340f1-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="340f1-149">En el portal de Azure, en Hola Hola **etouches** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="340f1-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="340f1-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="340f1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="340f1-153">En hello **etouches dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="340f1-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="340f1-155">a.</span><span class="sxs-lookup"><span data-stu-id="340f1-155">a.</span></span> <span data-ttu-id="340f1-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="340f1-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="340f1-157">b.</span><span class="sxs-lookup"><span data-stu-id="340f1-157">b.</span></span> <span data-ttu-id="340f1-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="340f1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="340f1-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="340f1-159">These values are not real.</span></span> <span data-ttu-id="340f1-160">Actualizar el valor de hello con hello real iniciar sesión en la dirección URL y el identificador, que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="340f1-161">aplicación de etouches espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="340f1-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="340f1-162">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="340f1-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="340f1-163">Puede administrar valores de hello de estos atributos de hello **usuario atributo** de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="340f1-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="340f1-164">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="340f1-164">hello following screenshot shows an example for this.</span></span> 

    ![Atributo de usuario](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="340f1-166">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="340f1-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="340f1-167">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="340f1-167">Attribute Name</span></span> | <span data-ttu-id="340f1-168">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="340f1-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="340f1-169">Email</span><span class="sxs-lookup"><span data-stu-id="340f1-169">Email</span></span> | <span data-ttu-id="340f1-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="340f1-170">user.mail</span></span> |    
    
    <span data-ttu-id="340f1-171">a.</span><span class="sxs-lookup"><span data-stu-id="340f1-171">a.</span></span> <span data-ttu-id="340f1-172">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="340f1-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Agregar atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Cuadro de diálogo Agregar atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="340f1-175">b.</span><span class="sxs-lookup"><span data-stu-id="340f1-175">b.</span></span> <span data-ttu-id="340f1-176">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="340f1-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="340f1-177">c.</span><span class="sxs-lookup"><span data-stu-id="340f1-177">c.</span></span> <span data-ttu-id="340f1-178">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="340f1-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="340f1-179">d.</span><span class="sxs-lookup"><span data-stu-id="340f1-179">d.</span></span> <span data-ttu-id="340f1-180">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="340f1-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="340f1-181">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="340f1-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="340f1-183">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="340f1-183">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="340f1-185">tooget SSO configurado para la aplicación, lleve a cabo Hola siguiendo los pasos de hello etouches aplicación:</span><span class="sxs-lookup"><span data-stu-id="340f1-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![Configuración de etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="340f1-187">a.</span><span class="sxs-lookup"><span data-stu-id="340f1-187">a.</span></span> <span data-ttu-id="340f1-188">Inicio de sesión demasiado**etouches** aplicación con derechos de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="340f1-189">b.</span><span class="sxs-lookup"><span data-stu-id="340f1-189">b.</span></span> <span data-ttu-id="340f1-190">Vaya toohello **SAML** configuración.</span><span class="sxs-lookup"><span data-stu-id="340f1-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="340f1-191">c.</span><span class="sxs-lookup"><span data-stu-id="340f1-191">c.</span></span> <span data-ttu-id="340f1-192">Hola **configuración General** sección, abra el certificado descargado desde el portal de Azure en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en el cuadro de texto de hello IDP metadatos.</span><span class="sxs-lookup"><span data-stu-id="340f1-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="340f1-193">d.</span><span class="sxs-lookup"><span data-stu-id="340f1-193">d.</span></span> <span data-ttu-id="340f1-194">Haga clic en hello **Guardar & permanecen** botón.</span><span class="sxs-lookup"><span data-stu-id="340f1-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="340f1-195">e.</span><span class="sxs-lookup"><span data-stu-id="340f1-195">e.</span></span> <span data-ttu-id="340f1-196">Haga clic en hello **metadatos de actualización** botón Hola sección de metadatos de SAML.</span><span class="sxs-lookup"><span data-stu-id="340f1-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="340f1-197">f.</span><span class="sxs-lookup"><span data-stu-id="340f1-197">f.</span></span> <span data-ttu-id="340f1-198">Se abrirá Hola página y efectuar el SSO.</span><span class="sxs-lookup"><span data-stu-id="340f1-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="340f1-199">Una vez Hola SSO está trabajando, a continuación, puede configurar el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="340f1-200">g.</span><span class="sxs-lookup"><span data-stu-id="340f1-200">g.</span></span> <span data-ttu-id="340f1-201">En el campo de nombre de usuario de hello, seleccione hello **emailaddress** tal y como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="340f1-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="340f1-202">h.</span><span class="sxs-lookup"><span data-stu-id="340f1-202">h.</span></span> <span data-ttu-id="340f1-203">Hola copia **Id. de entidad de SP** valor y pegarlo en hello **identificador** cuadro de texto, que se encuentra en **etouches dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="340f1-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="340f1-204">i.</span><span class="sxs-lookup"><span data-stu-id="340f1-204">i.</span></span> <span data-ttu-id="340f1-205">Hola copia **dirección URL SSO / ACS** valor y pegarlo en hello **dirección URL de inicio de sesión** cuadro de texto, que se encuentra en **etouches dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="340f1-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="340f1-206">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="340f1-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="340f1-207">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="340f1-208">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="340f1-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="340f1-209">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="340f1-209">Create an Azure AD test user</span></span>
<span data-ttu-id="340f1-210">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="340f1-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="340f1-212">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="340f1-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="340f1-213">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="340f1-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="340f1-215">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="340f1-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="340f1-217">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="340f1-219">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="340f1-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="340f1-221">a.</span><span class="sxs-lookup"><span data-stu-id="340f1-221">a.</span></span> <span data-ttu-id="340f1-222">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="340f1-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="340f1-223">b.</span><span class="sxs-lookup"><span data-stu-id="340f1-223">b.</span></span> <span data-ttu-id="340f1-224">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="340f1-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="340f1-225">c.</span><span class="sxs-lookup"><span data-stu-id="340f1-225">c.</span></span> <span data-ttu-id="340f1-226">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="340f1-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="340f1-227">d.</span><span class="sxs-lookup"><span data-stu-id="340f1-227">d.</span></span> <span data-ttu-id="340f1-228">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="340f1-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="340f1-229">Creación de un usuario de prueba de etouches</span><span class="sxs-lookup"><span data-stu-id="340f1-229">Create an etouches test user</span></span>

<span data-ttu-id="340f1-230">En esta sección, se crea un usuario denominado Britta Simon en etouches.</span><span class="sxs-lookup"><span data-stu-id="340f1-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="340f1-231">Trabajar con [equipo de soporte técnico etouches cliente](https://www.etouches.com/event-software/support/customer-support/) a los usuarios de tooadd hello en la plataforma de etouches Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="340f1-232">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="340f1-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="340f1-233">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooetouches.</span><span class="sxs-lookup"><span data-stu-id="340f1-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="340f1-235">**tooassign Britta Simon tooetouches, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="340f1-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="340f1-236">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="340f1-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="340f1-238">En la lista de aplicaciones de hello, seleccione **etouches**.</span><span class="sxs-lookup"><span data-stu-id="340f1-238">In hello applications list, select **etouches**.</span></span>

    ![Hola etouches vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="340f1-240">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="340f1-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="340f1-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="340f1-242">Click **Add** button.</span></span> <span data-ttu-id="340f1-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="340f1-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="340f1-245">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="340f1-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="340f1-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="340f1-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="340f1-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="340f1-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="340f1-248">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="340f1-248">Test single sign-on</span></span>


<span data-ttu-id="340f1-249">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="340f1-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="340f1-250">Al hacer clic en hello etouches el icono Panel de acceso de hello, deberá obtener automáticamente ha iniciado sesión tooyour etouches aplicación.</span><span class="sxs-lookup"><span data-stu-id="340f1-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="340f1-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="340f1-251">Additional resources</span></span>

* [<span data-ttu-id="340f1-252">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="340f1-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="340f1-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="340f1-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

