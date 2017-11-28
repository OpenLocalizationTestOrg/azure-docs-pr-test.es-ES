---
title: "Tutorial: Integración de Azure Active Directory con Rally Software | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="17074-103">Tutorial: Integración de Azure Active Directory con Rally Software</span><span class="sxs-lookup"><span data-stu-id="17074-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="17074-104">En este tutorial, aprenderá cómo toointegrate Rally Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17074-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17074-105">Integración de Rally Software con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="17074-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17074-106">Puede controlar en Azure AD que tenga acceso tooRally Software.</span><span class="sxs-lookup"><span data-stu-id="17074-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="17074-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRally Software (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17074-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="17074-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17074-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="17074-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17074-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17074-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="17074-110">Prerequisites</span></span>

<span data-ttu-id="17074-111">integración de Azure AD con Rally Software tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="17074-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="17074-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17074-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17074-113">Una suscripción habilitada para el inicio de sesión único en Rally Software</span><span class="sxs-lookup"><span data-stu-id="17074-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17074-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="17074-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17074-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="17074-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17074-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="17074-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17074-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17074-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17074-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="17074-118">Scenario description</span></span>
<span data-ttu-id="17074-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="17074-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17074-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="17074-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17074-121">Agregar Rally Software desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="17074-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="17074-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17074-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="17074-123">Agregar Rally Software desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="17074-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="17074-124">integración de hello tooconfigure de Rally Software en Azure AD, deberá tooadd Rally Software de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="17074-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17074-125">**tooadd Rally Software desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17074-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17074-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="17074-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="17074-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="17074-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17074-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17074-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="17074-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17074-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="17074-133">En el cuadro de búsqueda de hello, escriba **Rally Software**, seleccione **Rally Software** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="17074-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Rally Software en la lista de resultados de Hola](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="17074-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="17074-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="17074-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Rally Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="17074-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17074-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Rally Software es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17074-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="17074-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Rally Software necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="17074-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="17074-139">En Rally Software, asignar el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="17074-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="17074-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Rally Software, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="17074-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17074-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="17074-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17074-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17074-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17074-143">**[Crear un usuario de prueba de Rally Software](#create-a-rally-software-test-user)**  -toohave un equivalente de Britta Simon en Rally Software que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="17074-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17074-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="17074-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17074-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="17074-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="17074-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17074-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="17074-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Rally Software.</span><span class="sxs-lookup"><span data-stu-id="17074-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="17074-148">**inicio de sesión único en tooconfigure Azure AD con Rally Software, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17074-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="17074-149">En el portal de Azure, en Hola Hola **Rally Software** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="17074-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="17074-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="17074-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="17074-153">En hello **Rally Software dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="17074-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="17074-155">a.</span><span class="sxs-lookup"><span data-stu-id="17074-155">a.</span></span> <span data-ttu-id="17074-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="17074-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="17074-157">b.</span><span class="sxs-lookup"><span data-stu-id="17074-157">b.</span></span> <span data-ttu-id="17074-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="17074-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17074-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="17074-159">These values are not real.</span></span> <span data-ttu-id="17074-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="17074-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="17074-161">Póngase en contacto con [equipo de soporte técnico de Rally Software cliente](https://help.rallydev.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="17074-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="17074-162">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="17074-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="17074-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="17074-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17074-166">En hello **Rally Software configuración** sección, haga clic en **configurar Rally Software** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="17074-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="17074-167">Hola copia **dirección URL de cierre de sesión y el Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="17074-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuración de Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="17074-169">Inicie sesión en tooyour **Rally Software** inquilino.</span><span class="sxs-lookup"><span data-stu-id="17074-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="17074-170">En la barra de herramientas de hello en la parte superior de hello, haga clic en **el programa de instalación**y, a continuación, seleccione **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="17074-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="17074-171">![Suscripción](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Suscripción")</span><span class="sxs-lookup"><span data-stu-id="17074-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="17074-172">Haga clic en hello **acción** botón.</span><span class="sxs-lookup"><span data-stu-id="17074-172">Click hello **Action** button.</span></span> <span data-ttu-id="17074-173">Seleccione **Editar suscripción** en hello lado superior derecho de la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="17074-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="17074-174">En hello **suscripción** página del cuadro de diálogo, realizar pasos de hello y, a continuación, haga clic en **guardar y cerrar**:</span><span class="sxs-lookup"><span data-stu-id="17074-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="17074-175">![Autenticación](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="17074-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="17074-176">a.</span><span class="sxs-lookup"><span data-stu-id="17074-176">a.</span></span> <span data-ttu-id="17074-177">Seleccione **Rally o autenticación de SSO** en la lista desplegable de autenticación.</span><span class="sxs-lookup"><span data-stu-id="17074-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="17074-178">b.</span><span class="sxs-lookup"><span data-stu-id="17074-178">b.</span></span> <span data-ttu-id="17074-179">Hola **dirección URL del proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17074-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="17074-180">c.</span><span class="sxs-lookup"><span data-stu-id="17074-180">c.</span></span> <span data-ttu-id="17074-181">Hola **cierre de sesión SSO** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17074-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="17074-182">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="17074-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17074-183">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="17074-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17074-184">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17074-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="17074-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17074-185">Create an Azure AD test user</span></span>

<span data-ttu-id="17074-186">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="17074-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="17074-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17074-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17074-189">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="17074-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="17074-191">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="17074-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="17074-193">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17074-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="17074-195">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="17074-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="17074-197">a.</span><span class="sxs-lookup"><span data-stu-id="17074-197">a.</span></span> <span data-ttu-id="17074-198">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17074-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17074-199">b.</span><span class="sxs-lookup"><span data-stu-id="17074-199">b.</span></span> <span data-ttu-id="17074-200">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17074-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="17074-201">c.</span><span class="sxs-lookup"><span data-stu-id="17074-201">c.</span></span> <span data-ttu-id="17074-202">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="17074-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="17074-203">d.</span><span class="sxs-lookup"><span data-stu-id="17074-203">d.</span></span> <span data-ttu-id="17074-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="17074-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="17074-205">Creación de un usuario de prueba de Rally Software</span><span class="sxs-lookup"><span data-stu-id="17074-205">Create a Rally Software test user</span></span>

<span data-ttu-id="17074-206">Para Azure AD a los usuarios toobe puede toosign en, deben ser aprovisionado toohello aplicación Rally Software con sus nombres de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="17074-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="17074-207">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17074-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="17074-208">Inicie sesión en tooyour inquilino de Rally Software.</span><span class="sxs-lookup"><span data-stu-id="17074-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="17074-209">Vaya demasiado**el programa de instalación \> usuarios**y, a continuación, haga clic en **+ Agregar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="17074-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="17074-210">![Usuarios](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="17074-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="17074-211">Escriba el nombre de hello en el cuadro de texto de hello nuevo usuario y, a continuación, haga clic en **agregar con detalles**.</span><span class="sxs-lookup"><span data-stu-id="17074-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="17074-212">Hola **Create User** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="17074-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="17074-213">![Creación de usuarios](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="17074-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="17074-214">a.</span><span class="sxs-lookup"><span data-stu-id="17074-214">a.</span></span> <span data-ttu-id="17074-215">Hola **nombre de usuario** cuadro de texto Nombre de usuario como Hola de tipo **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="17074-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="17074-216">b.</span><span class="sxs-lookup"><span data-stu-id="17074-216">b.</span></span> <span data-ttu-id="17074-217">En **dirección de correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="17074-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="17074-218">c.</span><span class="sxs-lookup"><span data-stu-id="17074-218">c.</span></span> <span data-ttu-id="17074-219">En **nombre** texto cuadro, escriba Hola nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="17074-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="17074-220">d.</span><span class="sxs-lookup"><span data-stu-id="17074-220">d.</span></span> <span data-ttu-id="17074-221">En **Last Name** texto cuadro, escriba Hola último nombre de usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="17074-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="17074-222">e.</span><span class="sxs-lookup"><span data-stu-id="17074-222">e.</span></span> <span data-ttu-id="17074-223">Haga clic en **Guardar y cerrar**.</span><span class="sxs-lookup"><span data-stu-id="17074-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="17074-224">Puede usar cualquier otra Rally Software usuario cuenta herramienta de creación o las API proporcionadas por Rally Software tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17074-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="17074-225">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17074-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="17074-226">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRally Software.</span><span class="sxs-lookup"><span data-stu-id="17074-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="17074-228">**tooassign Britta Simon tooRally Software, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17074-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="17074-229">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17074-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="17074-231">En la lista de aplicaciones de hello, seleccione **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="17074-231">In hello applications list, select **Rally Software**.</span></span>

    ![vínculo de Rally Software Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="17074-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17074-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="17074-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="17074-235">Click **Add** button.</span></span> <span data-ttu-id="17074-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17074-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="17074-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="17074-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17074-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17074-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17074-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17074-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="17074-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="17074-241">Test single sign-on</span></span>

<span data-ttu-id="17074-242">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="17074-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="17074-243">Al hacer clic en icono de Rally Software Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Rally Software.</span><span class="sxs-lookup"><span data-stu-id="17074-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17074-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="17074-244">Additional resources</span></span>

* [<span data-ttu-id="17074-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17074-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17074-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17074-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

