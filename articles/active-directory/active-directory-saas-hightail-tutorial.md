---
title: "Tutorial: integración de Azure Active Directory con Hightail | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="56ec6-103">Tutorial: Integración de Azure Active Directory con Hightail</span><span class="sxs-lookup"><span data-stu-id="56ec6-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="56ec6-104">En este tutorial, aprenderá cómo toointegrate Hightail con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56ec6-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56ec6-105">Integración Hightail con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="56ec6-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="56ec6-106">Puede controlar en Azure AD que tenga acceso tooHightail</span><span class="sxs-lookup"><span data-stu-id="56ec6-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="56ec6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHightail (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ec6-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56ec6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="56ec6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="56ec6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56ec6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56ec6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="56ec6-110">Prerequisites</span></span>

<span data-ttu-id="56ec6-111">integración de Azure AD con Hightail tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="56ec6-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="56ec6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ec6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56ec6-113">Una suscripción habilitada para el inicio de sesión único en Hightail</span><span class="sxs-lookup"><span data-stu-id="56ec6-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56ec6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="56ec6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56ec6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="56ec6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56ec6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="56ec6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56ec6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56ec6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56ec6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="56ec6-118">Scenario description</span></span>
<span data-ttu-id="56ec6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="56ec6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56ec6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="56ec6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56ec6-121">Agregar Hightail desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="56ec6-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="56ec6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ec6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="56ec6-123">Agregar Hightail desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="56ec6-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="56ec6-124">integración de hello tooconfigure de Hightail en Azure AD, deberá tooadd Hightail de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="56ec6-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="56ec6-125">**tooadd Hightail de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56ec6-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="56ec6-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="56ec6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56ec6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="56ec6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="56ec6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56ec6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="56ec6-133">En el cuadro de búsqueda de hello, escriba **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-133">In hello search box, type **Hightail**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="56ec6-135">En el panel de resultados de hello, seleccione **Hightail**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="56ec6-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56ec6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ec6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56ec6-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Hightail con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56ec6-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56ec6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Hightail es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56ec6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="56ec6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Hightail debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="56ec6-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="56ec6-141">En Hightail, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="56ec6-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="56ec6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Hightail, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="56ec6-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="56ec6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="56ec6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="56ec6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56ec6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56ec6-145">**[Crear un usuario de prueba Hightail](#creating-a-hightail-test-user)**  -toohave un equivalente de Britta Simon en Hightail que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="56ec6-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="56ec6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="56ec6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56ec6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="56ec6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56ec6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ec6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56ec6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Hightail.</span><span class="sxs-lookup"><span data-stu-id="56ec6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="56ec6-150">**inicio de sesión único en Azure AD tooconfigure con Hightail, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56ec6-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="56ec6-151">En el portal de Azure, en Hola Hola **Hightail** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="56ec6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="56ec6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="56ec6-155">En hello **Hightail dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="56ec6-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="56ec6-157">Hola **dirección URL de respuesta** cuadro de texto, escriba la dirección URL hello como:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="56ec6-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56ec6-158">Hello valor anterior no es un valor real.</span><span class="sxs-lookup"><span data-stu-id="56ec6-158">hello preceding value is not real value.</span></span> <span data-ttu-id="56ec6-159">Se actualizará el valor de hello con URL de respuesta real hello, que se explica más adelante en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="56ec6-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="56ec6-160">En hello **Hightail dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="56ec6-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="56ec6-162">a.</span><span class="sxs-lookup"><span data-stu-id="56ec6-162">a.</span></span> <span data-ttu-id="56ec6-163">Haga clic en hello **mostrar avanzadas de configuración de la URL**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="56ec6-164">b.</span><span class="sxs-lookup"><span data-stu-id="56ec6-164">b.</span></span> <span data-ttu-id="56ec6-165">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello como:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="56ec6-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="56ec6-166">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="56ec6-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="56ec6-168">Hightail aplicación espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="56ec6-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="56ec6-169">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="56ec6-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="56ec6-170">Puede administrar valores de hello de estos atributos de hello **"Atrribute"** pestaña de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="56ec6-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="56ec6-171">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="56ec6-171">hello following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="56ec6-173">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="56ec6-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="56ec6-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="56ec6-174">Attribute Name</span></span> | <span data-ttu-id="56ec6-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="56ec6-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="56ec6-176">Nombre</span><span class="sxs-lookup"><span data-stu-id="56ec6-176">FirstName</span></span> | <span data-ttu-id="56ec6-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="56ec6-177">user.givenname</span></span> |
    | <span data-ttu-id="56ec6-178">Apellidos</span><span class="sxs-lookup"><span data-stu-id="56ec6-178">LastName</span></span> | <span data-ttu-id="56ec6-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="56ec6-179">user.surname</span></span> |
    | <span data-ttu-id="56ec6-180">Email</span><span class="sxs-lookup"><span data-stu-id="56ec6-180">Email</span></span> | <span data-ttu-id="56ec6-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="56ec6-181">user.mail</span></span> |    
    | <span data-ttu-id="56ec6-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="56ec6-182">UserIdentity</span></span> | <span data-ttu-id="56ec6-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="56ec6-183">user.mail</span></span> |
    
    <span data-ttu-id="56ec6-184">a.</span><span class="sxs-lookup"><span data-stu-id="56ec6-184">a.</span></span> <span data-ttu-id="56ec6-185">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56ec6-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="56ec6-188">b.</span><span class="sxs-lookup"><span data-stu-id="56ec6-188">b.</span></span> <span data-ttu-id="56ec6-189">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="56ec6-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="56ec6-190">c.</span><span class="sxs-lookup"><span data-stu-id="56ec6-190">c.</span></span> <span data-ttu-id="56ec6-191">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="56ec6-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="56ec6-192">d.</span><span class="sxs-lookup"><span data-stu-id="56ec6-192">d.</span></span> <span data-ttu-id="56ec6-193">Deje hello **Namespace** en blanco.</span><span class="sxs-lookup"><span data-stu-id="56ec6-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="56ec6-194">e.</span><span class="sxs-lookup"><span data-stu-id="56ec6-194">e.</span></span> <span data-ttu-id="56ec6-195">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-195">Click **Ok**.</span></span>

7. <span data-ttu-id="56ec6-196">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="56ec6-196">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="56ec6-198">En hello **Hightail configuración** sección, haga clic en **configurar Hightail** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="56ec6-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="56ec6-199">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="56ec6-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="56ec6-201">Antes de configurar Hola inicio de sesión único en la aplicación Hightail, lista blanca de su dominio de correo electrónico con Hightail de equipo para que todos los usuarios que se usan este dominio de Hola puede use funcionalidad de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="56ec6-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="56ec6-202">tooget configurado para la aplicación de SSO, debe a toosign en tooyour Hightail inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="56ec6-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="56ec6-203">a.</span><span class="sxs-lookup"><span data-stu-id="56ec6-203">a.</span></span> <span data-ttu-id="56ec6-204">En el menú de hello en la parte superior de hello, haga clic en hello **cuenta** pestaña y seleccione **configurar SAML**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="56ec6-206">b.</span><span class="sxs-lookup"><span data-stu-id="56ec6-206">b.</span></span> <span data-ttu-id="56ec6-207">Casilla de Hola de **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="56ec6-209">c.</span><span class="sxs-lookup"><span data-stu-id="56ec6-209">c.</span></span> <span data-ttu-id="56ec6-210">Abra el certificado codificado en base 64 en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado de firma de tokens SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="56ec6-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="56ec6-212">d.</span><span class="sxs-lookup"><span data-stu-id="56ec6-212">d.</span></span> <span data-ttu-id="56ec6-213">Hola **autoridad de SAML (proveedor de identidades)** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** copiados desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ec6-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="56ec6-215">e.</span><span class="sxs-lookup"><span data-stu-id="56ec6-215">e.</span></span> <span data-ttu-id="56ec6-216">Si desea que aplicación de hello tooconfigure en **modo iniciado por IDP** seleccione **"Inicio de sesión iniciado por el proveedor de identidades (IdP)"**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="56ec6-217">Si prefiere el **modo iniciado por el proveedor de servicios**, seleccione **"Service Provider (SP) initiated log in"** ("Inicio de sesión iniciado por el proveedor de servicios").</span><span class="sxs-lookup"><span data-stu-id="56ec6-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="56ec6-219">f.</span><span class="sxs-lookup"><span data-stu-id="56ec6-219">f.</span></span> <span data-ttu-id="56ec6-220">Dirección URL del consumidor SAML de hello para la instancia de copiar y pegar en **dirección URL de respuesta** en el cuadro de texto **Hightail dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ec6-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="56ec6-221">g.</span><span class="sxs-lookup"><span data-stu-id="56ec6-221">g.</span></span> <span data-ttu-id="56ec6-222">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="56ec6-223">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="56ec6-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="56ec6-224">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="56ec6-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="56ec6-225">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56ec6-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56ec6-226">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ec6-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="56ec6-227">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="56ec6-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="56ec6-229">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56ec6-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="56ec6-230">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="56ec6-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56ec6-232">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56ec6-234">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="56ec6-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56ec6-236">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="56ec6-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56ec6-238">a.</span><span class="sxs-lookup"><span data-stu-id="56ec6-238">a.</span></span> <span data-ttu-id="56ec6-239">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56ec6-240">b.</span><span class="sxs-lookup"><span data-stu-id="56ec6-240">b.</span></span> <span data-ttu-id="56ec6-241">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56ec6-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56ec6-242">c.</span><span class="sxs-lookup"><span data-stu-id="56ec6-242">c.</span></span> <span data-ttu-id="56ec6-243">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="56ec6-244">d.</span><span class="sxs-lookup"><span data-stu-id="56ec6-244">d.</span></span> <span data-ttu-id="56ec6-245">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="56ec6-246">Crear un usuario de prueba de Hightail</span><span class="sxs-lookup"><span data-stu-id="56ec6-246">Creating a Hightail test user</span></span>

<span data-ttu-id="56ec6-247">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Hightail toocreate.</span><span class="sxs-lookup"><span data-stu-id="56ec6-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="56ec6-248">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="56ec6-248">There is no action item for you in this section.</span></span> <span data-ttu-id="56ec6-249">Hightail admite el aprovisionamiento de usuarios just-in-time basado en notificaciones personalizadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="56ec6-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="56ec6-250">Si ha configurado notificaciones personalizadas de hello tal y como se muestra en la sección de hello  **[configurar Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  los casos anteriores, automáticamente se crea un usuario en la aplicación hello no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="56ec6-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="56ec6-251">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="56ec6-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="56ec6-252">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ec6-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="56ec6-253">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHightail.</span><span class="sxs-lookup"><span data-stu-id="56ec6-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="56ec6-255">**tooassign Britta Simon tooHightail, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56ec6-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="56ec6-256">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="56ec6-258">En la lista de aplicaciones de hello, seleccione **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-258">In hello applications list, select **Hightail**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="56ec6-260">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="56ec6-262">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-262">Click **Add** button.</span></span> <span data-ttu-id="56ec6-263">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="56ec6-265">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="56ec6-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="56ec6-266">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56ec6-267">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="56ec6-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56ec6-268">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="56ec6-268">Testing single sign-on</span></span>

<span data-ttu-id="56ec6-269">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="56ec6-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="56ec6-270">Al hacer clic en icono de Hightail Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Hightail aplicación.</span><span class="sxs-lookup"><span data-stu-id="56ec6-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="56ec6-271">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="56ec6-271">Additional resources</span></span>

* [<span data-ttu-id="56ec6-272">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56ec6-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56ec6-273">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56ec6-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

