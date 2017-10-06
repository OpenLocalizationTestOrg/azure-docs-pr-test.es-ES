---
title: "Tutorial: Integración de Azure Active Directory con Lucidchart | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="52564-103">Tutorial: Integración de Azure Active Directory con Lucidchart</span><span class="sxs-lookup"><span data-stu-id="52564-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="52564-104">En este tutorial, aprenderá cómo toointegrate Lucidchart con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52564-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52564-105">Integración Lucidchart con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="52564-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52564-106">Puede controlar en Azure AD que tenga acceso tooLucidchart</span><span class="sxs-lookup"><span data-stu-id="52564-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="52564-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLucidchart (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52564-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52564-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="52564-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="52564-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52564-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52564-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52564-110">Prerequisites</span></span>

<span data-ttu-id="52564-111">integración de Azure AD con Lucidchart tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="52564-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="52564-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52564-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52564-113">Una suscripción habilitada para inicio de sesión único en Lucidchart</span><span class="sxs-lookup"><span data-stu-id="52564-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52564-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="52564-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52564-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="52564-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52564-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="52564-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52564-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52564-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52564-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="52564-118">Scenario description</span></span>
<span data-ttu-id="52564-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="52564-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52564-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="52564-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52564-121">Agregar Lucidchart desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="52564-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="52564-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52564-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="52564-123">Agregar Lucidchart desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="52564-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="52564-124">integración de hello tooconfigure de Lucidchart en Azure AD, deberá tooadd Lucidchart de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="52564-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52564-125">**tooadd Lucidchart de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52564-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52564-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="52564-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52564-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="52564-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52564-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52564-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="52564-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52564-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="52564-133">En el cuadro de búsqueda de hello, escriba **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="52564-133">In hello search box, type **Lucidchart**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="52564-135">En el panel de resultados de hello, seleccione **Lucidchart**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="52564-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52564-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52564-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52564-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Lucidchart con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52564-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52564-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Lucidchart es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52564-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="52564-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Lucidchart debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="52564-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="52564-141">En Lucidchart, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52564-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52564-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Lucidchart, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="52564-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52564-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="52564-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52564-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52564-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52564-145">**[Crear un usuario de prueba de Lucidchart](#creating-a-lucidchart-test-user)**  -toohave un equivalente de Britta Simon en Lucidchart que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="52564-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52564-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="52564-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52564-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="52564-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52564-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52564-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52564-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="52564-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="52564-150">**inicio de sesión único en Azure AD tooconfigure con Lucidchart, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52564-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="52564-151">En el portal de Azure, en Hola Hola **Lucidchart** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="52564-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="52564-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="52564-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="52564-155">En hello **Lucidchart dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="52564-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="52564-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="52564-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="52564-158">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="52564-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="52564-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="52564-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52564-162">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="52564-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="52564-163">En el menú de hello en la parte superior de hello, haga clic en **equipo**.</span><span class="sxs-lookup"><span data-stu-id="52564-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="52564-164">![Equipo](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Equipo")</span><span class="sxs-lookup"><span data-stu-id="52564-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="52564-165">Haga clic en **Applications \> (Aplicaciones) Manage SAML** (Administrar SAML).</span><span class="sxs-lookup"><span data-stu-id="52564-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="52564-166">![Administrar SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Administrar SAML")</span><span class="sxs-lookup"><span data-stu-id="52564-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="52564-167">En hello **SAML Authentication Settings** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="52564-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="52564-168">a.</span><span class="sxs-lookup"><span data-stu-id="52564-168">a.</span></span> <span data-ttu-id="52564-169">Seleccione **Habilitar autenticación SAML** y, después, haga clic en **Opcional**.</span><span class="sxs-lookup"><span data-stu-id="52564-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="52564-170">![Configuración de la autenticación SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "Configuración de la autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="52564-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="52564-171">b.</span><span class="sxs-lookup"><span data-stu-id="52564-171">b.</span></span> <span data-ttu-id="52564-172">Hola **dominio** cuadro de texto, escriba su dominio y, a continuación, haga clic en **Cambiar certificado**.</span><span class="sxs-lookup"><span data-stu-id="52564-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="52564-173">![Cambiar certificado](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Cambiar certificado")</span><span class="sxs-lookup"><span data-stu-id="52564-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="52564-174">c.</span><span class="sxs-lookup"><span data-stu-id="52564-174">c.</span></span> <span data-ttu-id="52564-175">Abra el archivo de metadatos descargado, Hola copia contenido y, a continuación, péguelo en hello **cargar metadatos** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="52564-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="52564-176">![Cargar metadatos](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Cargar metadatos")</span><span class="sxs-lookup"><span data-stu-id="52564-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="52564-177">d.</span><span class="sxs-lookup"><span data-stu-id="52564-177">d.</span></span> <span data-ttu-id="52564-178">Seleccione **automáticamente Agregar nuevo grupo de usuarios toohello**y, a continuación, haga clic en **guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="52564-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="52564-179">![Guardar cambios](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Guardar cambios")</span><span class="sxs-lookup"><span data-stu-id="52564-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="52564-180">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="52564-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52564-181">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="52564-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52564-182">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52564-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52564-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52564-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="52564-184">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="52564-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="52564-186">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52564-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52564-187">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="52564-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52564-189">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="52564-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52564-191">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52564-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52564-193">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="52564-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52564-195">a.</span><span class="sxs-lookup"><span data-stu-id="52564-195">a.</span></span> <span data-ttu-id="52564-196">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52564-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52564-197">b.</span><span class="sxs-lookup"><span data-stu-id="52564-197">b.</span></span> <span data-ttu-id="52564-198">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52564-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52564-199">c.</span><span class="sxs-lookup"><span data-stu-id="52564-199">c.</span></span> <span data-ttu-id="52564-200">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="52564-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="52564-201">d.</span><span class="sxs-lookup"><span data-stu-id="52564-201">d.</span></span> <span data-ttu-id="52564-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="52564-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="52564-203">Creación de un usuario de prueba de Lucidchart</span><span class="sxs-lookup"><span data-stu-id="52564-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="52564-204">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="52564-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="52564-205">Cuando un usuario asignado intenta toolog en Lucidchart a través de panel de acceso de hello, Lucidchart comprueba si existe el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="52564-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="52564-206">Si no hay cuentas de usuario disponibles, Lucidchart crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="52564-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="52564-207">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="52564-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="52564-208">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="52564-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="52564-210">**tooassign Britta Simon tooLucidchart, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52564-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="52564-211">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52564-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="52564-213">En la lista de aplicaciones de hello, seleccione **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="52564-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="52564-215">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52564-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="52564-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="52564-217">Click **Add** button.</span></span> <span data-ttu-id="52564-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52564-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="52564-220">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="52564-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52564-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52564-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52564-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52564-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52564-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="52564-223">Testing single sign-on</span></span>

<span data-ttu-id="52564-224">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="52564-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="52564-225">Al hacer clic en icono de Lucidchart Hola Hola Panel de acceso, deberá obtener la aplicación de Lucidchart tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="52564-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="52564-226">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52564-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52564-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="52564-227">Additional resources</span></span>

* [<span data-ttu-id="52564-228">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52564-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52564-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52564-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

