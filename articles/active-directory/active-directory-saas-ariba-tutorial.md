---
title: "Tutorial: Integración de Azure Active Directory con Ariba | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: a1b17129c1298b59c155a0890e41e41ff9544a24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="5d2b9-103">Tutorial: Integración de Azure Active Directory con Ariba</span><span class="sxs-lookup"><span data-stu-id="5d2b9-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="5d2b9-104">En este tutorial, aprenderá cómo toointegrate Ariba con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d2b9-104">In this tutorial, you learn how toointegrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d2b9-105">Integración Ariba con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5d2b9-105">Integrating Ariba with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d2b9-106">Puede controlar en Azure AD que tenga acceso tooAriba</span><span class="sxs-lookup"><span data-stu-id="5d2b9-106">You can control in Azure AD who has access tooAriba</span></span>
- <span data-ttu-id="5d2b9-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAriba (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d2b9-107">You can enable your users tooautomatically get signed-on tooAriba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d2b9-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5d2b9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5d2b9-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d2b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d2b9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5d2b9-110">Prerequisites</span></span>

<span data-ttu-id="5d2b9-111">integración de Azure AD con Ariba tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5d2b9-111">tooconfigure Azure AD integration with Ariba, you need hello following items:</span></span>

- <span data-ttu-id="5d2b9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d2b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d2b9-113">Una suscripción habilitada para el inicio de sesión único en Ariba</span><span class="sxs-lookup"><span data-stu-id="5d2b9-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d2b9-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d2b9-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5d2b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d2b9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d2b9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d2b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d2b9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5d2b9-118">Scenario description</span></span>
<span data-ttu-id="5d2b9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d2b9-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5d2b9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d2b9-121">Agregar Ariba desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5d2b9-121">Adding Ariba from hello gallery</span></span>
2. <span data-ttu-id="5d2b9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d2b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-hello-gallery"></a><span data-ttu-id="5d2b9-123">Agregar Ariba desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5d2b9-123">Adding Ariba from hello gallery</span></span>
<span data-ttu-id="5d2b9-124">integración de hello tooconfigure de Ariba en Azure AD, deberá tooadd Ariba de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-124">tooconfigure hello integration of Ariba into Azure AD, you need tooadd Ariba from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d2b9-125">**tooadd Ariba de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d2b9-125">**tooadd Ariba from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d2b9-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d2b9-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d2b9-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5d2b9-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5d2b9-133">En el cuadro de búsqueda de hello, escriba **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-133">In hello search box, type **Ariba**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="5d2b9-135">En el panel de resultados de hello, seleccione **Ariba**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-135">In hello results panel, select **Ariba**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d2b9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d2b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d2b9-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Ariba con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5d2b9-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5d2b9-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Ariba es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ariba is tooa user in Azure AD.</span></span> <span data-ttu-id="5d2b9-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Ariba debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-140">In other words, a link relationship between an Azure AD user and hello related user in Ariba needs toobe established.</span></span>

<span data-ttu-id="5d2b9-141">En Ariba, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-141">In Ariba, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d2b9-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Ariba, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5d2b9-142">tooconfigure and test Azure AD single sign-on with Ariba, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d2b9-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d2b9-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d2b9-145">**[Creación de un usuario de prueba Ariba](#creating-an-ariba-test-user)**  -toohave un equivalente de Britta Simon en Ariba que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - toohave a counterpart of Britta Simon in Ariba that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d2b9-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d2b9-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d2b9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d2b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d2b9-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Ariba.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="5d2b9-150">**inicio de sesión único en Azure AD tooconfigure con Ariba, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d2b9-150">**tooconfigure Azure AD single sign-on with Ariba, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d2b9-151">En el portal de Azure, en Hola Hola **Ariba** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-151">In hello Azure portal, on hello **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5d2b9-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="5d2b9-155">En hello **Ariba dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5d2b9-155">On hello **Ariba Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="5d2b9-157">a.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-157">a.</span></span> <span data-ttu-id="5d2b9-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: `https://<subdomain>.sourcing.ariba.com` o`https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="5d2b9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="5d2b9-159">b.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-159">b.</span></span> <span data-ttu-id="5d2b9-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="5d2b9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d2b9-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-161">These values are not real.</span></span> <span data-ttu-id="5d2b9-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5d2b9-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="5d2b9-164">Póngase en contacto con el equipo de soporte técnico de cliente Ariba en **1-866-218-2155** tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-164">Contact Ariba Client support team at **1-866-218-2155** tooget these values.</span></span> 
 

4. <span data-ttu-id="5d2b9-165">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate  file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="5d2b9-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5d2b9-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5d2b9-169">tooget SSO configurado para la aplicación, llame al equipo de soporte técnico de Ariba en **1-866-218-2155** y podrá ayudarle aún más en cómo se descarga tooprovide ellos Hola **certificado (Base64)** archivo.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-169">tooget SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how tooprovide them hello downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="5d2b9-170">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="5d2b9-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d2b9-171">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d2b9-172">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d2b9-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d2b9-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d2b9-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d2b9-174">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5d2b9-176">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d2b9-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d2b9-177">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d2b9-179">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d2b9-181">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d2b9-183">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5d2b9-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d2b9-185">a.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-185">a.</span></span> <span data-ttu-id="5d2b9-186">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d2b9-187">b.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-187">b.</span></span> <span data-ttu-id="5d2b9-188">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d2b9-189">c.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-189">c.</span></span> <span data-ttu-id="5d2b9-190">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5d2b9-191">d.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-191">d.</span></span> <span data-ttu-id="5d2b9-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="5d2b9-193">Creación de un usuario de prueba de Ariba</span><span class="sxs-lookup"><span data-stu-id="5d2b9-193">Creating an Ariba test user</span></span>

<span data-ttu-id="5d2b9-194">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Ariba toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-194">hello objective of this section is toocreate a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="5d2b9-195">Trabajar con el equipo de soporte técnico de Ariba en **1-866-218-2155** a los usuarios de tooadd Hola Hola Ariba sistema.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-195">Work with Ariba support team at **1-866-218-2155** tooadd hello users in hello Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="5d2b9-196">Si necesita un usuario toocreate manualmente, necesita toocontact equipo de soporte técnico de Ariba de hello en **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-196">If you need toocreate a user manually, you need toocontact hello Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5d2b9-197">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d2b9-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5d2b9-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAriba.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAriba.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5d2b9-200">**tooassign Britta Simon tooAriba, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d2b9-200">**tooassign Britta Simon tooAriba, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d2b9-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5d2b9-203">En la lista de aplicaciones de hello, seleccione **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-203">In hello applications list, select **Ariba**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="5d2b9-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5d2b9-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-207">Click **Add** button.</span></span> <span data-ttu-id="5d2b9-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5d2b9-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d2b9-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d2b9-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d2b9-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5d2b9-213">Testing single sign-on</span></span>
<span data-ttu-id="5d2b9-214">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5d2b9-215">Al hacer clic en icono de Ariba Hola Hola Panel de acceso, deberá obtener aplicaciones de Ariba tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="5d2b9-215">When you click hello Ariba tile in hello Access Panel, you should get automatically signed-on tooyour Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5d2b9-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5d2b9-216">Additional resources</span></span>

* [<span data-ttu-id="5d2b9-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d2b9-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d2b9-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5d2b9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

