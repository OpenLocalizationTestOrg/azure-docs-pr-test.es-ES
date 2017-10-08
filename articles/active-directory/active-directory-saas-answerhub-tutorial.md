---
title: "Tutorial: Integración de Azure Active Directory con AnswerHub | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="1de0b-103">Tutorial: Integración de Azure Active Directory con AnswerHub</span><span class="sxs-lookup"><span data-stu-id="1de0b-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="1de0b-104">En este tutorial, aprenderá cómo toointegrate AnswerHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1de0b-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1de0b-105">Integración de AnswerHub con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1de0b-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1de0b-106">Puede controlar en Azure AD que tenga acceso tooAnswerHub</span><span class="sxs-lookup"><span data-stu-id="1de0b-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="1de0b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAnswerHub (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1de0b-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1de0b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1de0b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1de0b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1de0b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1de0b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1de0b-110">Prerequisites</span></span>

<span data-ttu-id="1de0b-111">integración de Azure AD con AnswerHub tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1de0b-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="1de0b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1de0b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1de0b-113">Una suscripción habilitada para el inicio de sesión único en AnswerHub</span><span class="sxs-lookup"><span data-stu-id="1de0b-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1de0b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1de0b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1de0b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1de0b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1de0b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1de0b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1de0b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1de0b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1de0b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1de0b-118">Scenario description</span></span>
<span data-ttu-id="1de0b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1de0b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1de0b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="1de0b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1de0b-121">Adición de AnswerHub de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1de0b-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="1de0b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1de0b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="1de0b-123">Adición de AnswerHub de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1de0b-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="1de0b-124">integración de hello tooconfigure de AnswerHub en Azure AD, deberá tooadd AnswerHub de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="1de0b-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1de0b-125">**tooadd AnswerHub de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1de0b-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1de0b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1de0b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1de0b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1de0b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1de0b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1de0b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1de0b-133">En el cuadro de búsqueda de hello, escriba **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-133">In hello search box, type **AnswerHub**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="1de0b-135">En el panel de resultados de hello, seleccione **AnswerHub**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1de0b-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1de0b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1de0b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1de0b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AnswerHub con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1de0b-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1de0b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en AnswerHub es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1de0b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="1de0b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en AnswerHub debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="1de0b-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="1de0b-141">En AnswerHub, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1de0b-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1de0b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con AnswerHub, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1de0b-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1de0b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="1de0b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1de0b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1de0b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1de0b-145">**[Creación de un usuario de prueba de AnswerHub](#creating-an-answerhub-test-user)**  -toohave un equivalente de Britta Simon en AnswerHub que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="1de0b-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1de0b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1de0b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1de0b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1de0b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1de0b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1de0b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1de0b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="1de0b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="1de0b-150">**inicio de sesión único en Azure AD tooconfigure con AnswerHub, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1de0b-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="1de0b-151">En el portal de Azure, en Hola Hola **AnswerHub** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1de0b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1de0b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="1de0b-155">En hello **AnswerHub dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1de0b-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="1de0b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1de0b-157">a.</span></span> <span data-ttu-id="1de0b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="1de0b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="1de0b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1de0b-159">b.</span></span> <span data-ttu-id="1de0b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="1de0b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1de0b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1de0b-161">These values are not real.</span></span> <span data-ttu-id="1de0b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="1de0b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1de0b-163">Póngase en contacto con [equipo de soporte técnico de cliente de AnswerHub](mailto:success@answerhub.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="1de0b-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="1de0b-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1de0b-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="1de0b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1de0b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1de0b-168">En hello **configuración de AnswerHub** sección, haga clic en **configurar AnswerHub** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="1de0b-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1de0b-169">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="1de0b-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="1de0b-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de AnswerHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="1de0b-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1de0b-172">Si necesita ayuda para configurar AnswerHub, póngase en contacto con el [equipo de soporte técnico de AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="1de0b-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="1de0b-173">Vaya demasiado**administración**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="1de0b-174">Haga clic en hello **usuario y grupo** ficha.</span><span class="sxs-lookup"><span data-stu-id="1de0b-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="1de0b-175">En panel de navegación de hello en el lado izquierdo, en Hola de Hola **configuración de redes sociales** sección, haga clic en **configuración de SAML**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="1de0b-176">Haga clic en la pestaña **Configuración de IDP** .</span><span class="sxs-lookup"><span data-stu-id="1de0b-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="1de0b-177">En hello **configuración de IDP** , realice los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1de0b-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="1de0b-178">![Configuración de SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="1de0b-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="1de0b-179">a.</span><span class="sxs-lookup"><span data-stu-id="1de0b-179">a.</span></span> <span data-ttu-id="1de0b-180">En el cuadro de texto **IDP Login URL** (Dirección URL de inicio de sesión de IDP), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1de0b-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="1de0b-181">b.</span><span class="sxs-lookup"><span data-stu-id="1de0b-181">b.</span></span> <span data-ttu-id="1de0b-182">En el cuadro de texto **IDP Logout URL** (Dirección URL de cierre de sesión de IDP), pegue la **dirección URL de cierre de sesión** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1de0b-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="1de0b-183">c.</span><span class="sxs-lookup"><span data-stu-id="1de0b-183">c.</span></span> <span data-ttu-id="1de0b-184">En **formato del identificador de nombre IDP** cuadro de texto, escriba usuario Hola identificador igual valor seleccionado en el portal de Azure en **atributos de usuario** sección.</span><span class="sxs-lookup"><span data-stu-id="1de0b-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="1de0b-185">d.</span><span class="sxs-lookup"><span data-stu-id="1de0b-185">d.</span></span> <span data-ttu-id="1de0b-186">Haga clic en **Claves y certificados**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="1de0b-187">En la pestaña de claves y certificados de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1de0b-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="1de0b-188">![Claves y certificados](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Claves y certificados")</span><span class="sxs-lookup"><span data-stu-id="1de0b-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="1de0b-189">a.</span><span class="sxs-lookup"><span data-stu-id="1de0b-189">a.</span></span> <span data-ttu-id="1de0b-190">Abra el certificado codificado en base 64 que ha descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **clave pública IDP (formato x 509)** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="1de0b-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="1de0b-191">b.</span><span class="sxs-lookup"><span data-stu-id="1de0b-191">b.</span></span> <span data-ttu-id="1de0b-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-192">Click **Save**.</span></span>

14. <span data-ttu-id="1de0b-193">En hello **configuración de IDP** , haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1de0b-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="1de0b-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1de0b-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="1de0b-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1de0b-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1de0b-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1de0b-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1de0b-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="1de0b-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="1de0b-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1de0b-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1de0b-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1de0b-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1de0b-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1de0b-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1de0b-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1de0b-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1de0b-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1de0b-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1de0b-209">a.</span><span class="sxs-lookup"><span data-stu-id="1de0b-209">a.</span></span> <span data-ttu-id="1de0b-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1de0b-211">b.</span><span class="sxs-lookup"><span data-stu-id="1de0b-211">b.</span></span> <span data-ttu-id="1de0b-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1de0b-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1de0b-213">c.</span><span class="sxs-lookup"><span data-stu-id="1de0b-213">c.</span></span> <span data-ttu-id="1de0b-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1de0b-215">d.</span><span class="sxs-lookup"><span data-stu-id="1de0b-215">d.</span></span> <span data-ttu-id="1de0b-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="1de0b-217">Creación de un usuario de prueba de AnswerHub</span><span class="sxs-lookup"><span data-stu-id="1de0b-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="1de0b-218">toolog de los usuarios de Azure AD tooenable en tooAnswerHub, se les deben aprovisionar en AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="1de0b-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="1de0b-219">En caso de hello de AnswerHub, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="1de0b-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="1de0b-220">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1de0b-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1de0b-221">Inicie sesión en tooyour **AnswerHub** como administrador.</span><span class="sxs-lookup"><span data-stu-id="1de0b-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="1de0b-222">Vaya demasiado**administración**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="1de0b-223">Haga clic en hello **usuarios y grupos** ficha.</span><span class="sxs-lookup"><span data-stu-id="1de0b-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="1de0b-224">En panel de navegación de hello en el lado izquierdo, en Hola de Hola **administrar usuarios** sección, haga clic en **crear o importar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="1de0b-225">![Usuarios y grupos](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Usuarios y grupos")</span><span class="sxs-lookup"><span data-stu-id="1de0b-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="1de0b-226">Hola de tipo **dirección de correo electrónico**, **nombre de usuario** y **contraseña** de un Azure válida cuenta de Active Directory que quiera tooprovision en hello relacionados con cuadros de texto y, a continuación, haga clic en  **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1de0b-227">Puede usar cualquier otra AnswerHub usuario cuenta herramienta de creación o las API proporcionadas por AnswerHub tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="1de0b-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1de0b-228">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1de0b-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1de0b-229">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAnswerHub.</span><span class="sxs-lookup"><span data-stu-id="1de0b-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1de0b-231">**tooassign Britta Simon tooAnswerHub, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1de0b-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="1de0b-232">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1de0b-234">En la lista de aplicaciones de hello, seleccione **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="1de0b-236">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1de0b-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-238">Click **Add** button.</span></span> <span data-ttu-id="1de0b-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1de0b-241">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1de0b-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1de0b-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1de0b-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1de0b-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1de0b-244">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1de0b-244">Testing single sign-on</span></span>

<span data-ttu-id="1de0b-245">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1de0b-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1de0b-246">Al hacer clic en icono de AnswerHub de Hola Hola Panel de acceso, deberá obtener aplicaciones de AnswerHub de tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="1de0b-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="1de0b-247">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1de0b-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1de0b-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1de0b-248">Additional resources</span></span>

* [<span data-ttu-id="1de0b-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1de0b-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1de0b-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1de0b-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

