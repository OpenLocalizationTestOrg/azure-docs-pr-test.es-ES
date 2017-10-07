---
title: "Tutorial: Integración de Azure Active Directory con Picturepark | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="fd218-103">Tutorial: Integración de Azure Active Directory con Picturepark</span><span class="sxs-lookup"><span data-stu-id="fd218-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="fd218-104">En este tutorial, aprenderá cómo toointegrate Picturepark con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd218-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd218-105">Integración de Picturepark con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fd218-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fd218-106">Puede controlar en Azure AD que tenga acceso tooPicturepark</span><span class="sxs-lookup"><span data-stu-id="fd218-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="fd218-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPicturepark (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd218-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd218-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fd218-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fd218-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd218-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd218-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd218-110">Prerequisites</span></span>

<span data-ttu-id="fd218-111">integración de Azure AD con Picturepark tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fd218-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="fd218-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd218-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fd218-113">Una suscripción habilitada para el inicio de sesión único en Picturepark</span><span class="sxs-lookup"><span data-stu-id="fd218-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd218-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fd218-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd218-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fd218-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd218-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fd218-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd218-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd218-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd218-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fd218-118">Scenario description</span></span>
<span data-ttu-id="fd218-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fd218-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd218-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="fd218-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd218-121">Agregar Picturepark desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fd218-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="fd218-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd218-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="fd218-123">Agregar Picturepark desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fd218-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="fd218-124">integración de hello tooconfigure de Picturepark en Azure AD, deberá tooadd Picturepark de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="fd218-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fd218-125">**tooadd Picturepark de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fd218-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd218-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fd218-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd218-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fd218-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fd218-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fd218-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fd218-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fd218-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fd218-133">En el cuadro de búsqueda de hello, escriba **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="fd218-133">In hello search box, type **Picturepark**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="fd218-135">En el panel de resultados de hello, seleccione **Picturepark**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fd218-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd218-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd218-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd218-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Picturepark con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fd218-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fd218-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Picturepark es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd218-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="fd218-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Picturepark debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="fd218-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="fd218-141">En Picturepark, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fd218-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Picturepark, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fd218-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fd218-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="fd218-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fd218-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd218-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd218-145">**[Crear un usuario de prueba de Picturepark](#creating-a-picturepark-test-user) ** -toohave un equivalente de Britta Simon en Picturepark que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="fd218-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fd218-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fd218-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd218-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fd218-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd218-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd218-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd218-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Picturepark.</span><span class="sxs-lookup"><span data-stu-id="fd218-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="fd218-150">**inicio de sesión único en Azure AD tooconfigure con Picturepark, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fd218-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd218-151">En el portal de Azure, en Hola Hola **Picturepark** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fd218-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fd218-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fd218-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="fd218-155">En hello **Picturepark dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fd218-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="fd218-157">a.</span><span class="sxs-lookup"><span data-stu-id="fd218-157">a.</span></span> <span data-ttu-id="fd218-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="fd218-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="fd218-159">b.</span><span class="sxs-lookup"><span data-stu-id="fd218-159">b.</span></span> <span data-ttu-id="fd218-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="fd218-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="fd218-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="fd218-161">These values are not real.</span></span> <span data-ttu-id="fd218-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="fd218-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fd218-163">Póngase en contacto con [equipo de soporte técnico de cliente de Picturepark](https://picturepark.com/about/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="fd218-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="fd218-164">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="fd218-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="fd218-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fd218-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fd218-168">En hello **configuración de Picturepark** sección, haga clic en **configurar Picturepark** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="fd218-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fd218-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="fd218-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="fd218-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía Picturepark como administrador.</span><span class="sxs-lookup"><span data-stu-id="fd218-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="fd218-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en **herramientas administrativas**y, a continuación, haga clic en **consola de administración**.</span><span class="sxs-lookup"><span data-stu-id="fd218-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="fd218-173">![Consola de administración](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Consola de administración")</span><span class="sxs-lookup"><span data-stu-id="fd218-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="fd218-174">Haga clic en **Autenticación** y en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="fd218-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="fd218-175">![Autenticación](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="fd218-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="fd218-176">Hola **configuración del proveedor de identidades** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fd218-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fd218-177">![Configuración del proveedor de identidades](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuración del proveedor de identidades")</span><span class="sxs-lookup"><span data-stu-id="fd218-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="fd218-178">a.</span><span class="sxs-lookup"><span data-stu-id="fd218-178">a.</span></span> <span data-ttu-id="fd218-179">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fd218-179">Click **Add**.</span></span>
  
    <span data-ttu-id="fd218-180">b.</span><span class="sxs-lookup"><span data-stu-id="fd218-180">b.</span></span> <span data-ttu-id="fd218-181">Escriba un nombre para su configuración.</span><span class="sxs-lookup"><span data-stu-id="fd218-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="fd218-182">c.</span><span class="sxs-lookup"><span data-stu-id="fd218-182">c.</span></span> <span data-ttu-id="fd218-183">Seleccione **Establecer como predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="fd218-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="fd218-184">d.</span><span class="sxs-lookup"><span data-stu-id="fd218-184">d.</span></span> <span data-ttu-id="fd218-185">En **URI de emisor** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd218-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fd218-186">e.</span><span class="sxs-lookup"><span data-stu-id="fd218-186">e.</span></span> <span data-ttu-id="fd218-187">En **huella digital de emisor de confianza** cuadro de texto, pegue Hola valo **huella digital** que haya copiado desde **el certificado de firma de SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="fd218-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="fd218-188">Haga clic en **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="fd218-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="fd218-189">Hola tooset **Emailaddress** atributo Hola **notificación** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="fd218-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="fd218-190">![Configuración](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="fd218-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="fd218-191">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="fd218-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fd218-192">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fd218-193">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fd218-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd218-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd218-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="fd218-195">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="fd218-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fd218-197">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fd218-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd218-198">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fd218-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd218-200">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fd218-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd218-202">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd218-204">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="fd218-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd218-206">a.</span><span class="sxs-lookup"><span data-stu-id="fd218-206">a.</span></span> <span data-ttu-id="fd218-207">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd218-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd218-208">b.</span><span class="sxs-lookup"><span data-stu-id="fd218-208">b.</span></span> <span data-ttu-id="fd218-209">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fd218-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fd218-210">c.</span><span class="sxs-lookup"><span data-stu-id="fd218-210">c.</span></span> <span data-ttu-id="fd218-211">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fd218-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fd218-212">d.</span><span class="sxs-lookup"><span data-stu-id="fd218-212">d.</span></span> <span data-ttu-id="fd218-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fd218-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="fd218-214">Creación de un usuario de prueba de Picturepark</span><span class="sxs-lookup"><span data-stu-id="fd218-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="fd218-215">En orden tooenable toolog de los usuarios de Azure AD en Picturepark, se les deben aprovisionar en Picturepark.</span><span class="sxs-lookup"><span data-stu-id="fd218-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="fd218-216">En caso de hello de Picturepark, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="fd218-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="fd218-217">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fd218-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd218-218">Inicie sesión en tooyour **Picturepark** inquilino.</span><span class="sxs-lookup"><span data-stu-id="fd218-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="fd218-219">En la barra de herramientas de hello en la parte superior de hello, haga clic en **herramientas administrativas**y, a continuación, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fd218-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="fd218-220">![Usuarios](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="fd218-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="fd218-221">Hola **información general de los usuarios** , haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="fd218-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="fd218-222">![Administración de usuarios](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="fd218-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="fd218-223">En hello **Create User** cuadro de diálogo, realizar Hola siguiendo los pasos de un usuario válido de Azure Active Directory que desee tooprovision:</span><span class="sxs-lookup"><span data-stu-id="fd218-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="fd218-224">![Creación de usuarios](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="fd218-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="fd218-225">a.</span><span class="sxs-lookup"><span data-stu-id="fd218-225">a.</span></span> <span data-ttu-id="fd218-226">Hola **dirección de correo electrónico** cuadro de texto, hello tipo **dirección de correo electrónico** del usuario de hello ** BrittaSimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="fd218-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="fd218-227">b.</span><span class="sxs-lookup"><span data-stu-id="fd218-227">b.</span></span> <span data-ttu-id="fd218-228">Hola **contraseña** y **Confirmar contraseña** cuadros de texto, hello tipo **contraseña** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fd218-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="fd218-229">c.</span><span class="sxs-lookup"><span data-stu-id="fd218-229">c.</span></span> <span data-ttu-id="fd218-230">Hola **nombre** cuadro de texto, hello tipo **nombre** del usuario de hello **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="fd218-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="fd218-231">d.</span><span class="sxs-lookup"><span data-stu-id="fd218-231">d.</span></span> <span data-ttu-id="fd218-232">Hola **Last Name** cuadro de texto, hello tipo **Last Name** del usuario de hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fd218-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="fd218-233">e.</span><span class="sxs-lookup"><span data-stu-id="fd218-233">e.</span></span> <span data-ttu-id="fd218-234">Hola **empresa** cuadro de texto, hello tipo **nombre de la compañía** del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="fd218-235">f.</span><span class="sxs-lookup"><span data-stu-id="fd218-235">f.</span></span> <span data-ttu-id="fd218-236">Hola **país** cuadro de texto, seleccione hello **país** del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="fd218-237">g.</span><span class="sxs-lookup"><span data-stu-id="fd218-237">g.</span></span> <span data-ttu-id="fd218-238">Hola **código postal** cuadro de texto, hello tipo **código postal** de ciudad Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="fd218-239">h.</span><span class="sxs-lookup"><span data-stu-id="fd218-239">h.</span></span> <span data-ttu-id="fd218-240">Hola **City** cuadro de texto, hello tipo **nombre de la ciudad** del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="fd218-241">i.</span><span class="sxs-lookup"><span data-stu-id="fd218-241">i.</span></span> <span data-ttu-id="fd218-242">Seleccione un valor en **Language**(Idioma).</span><span class="sxs-lookup"><span data-stu-id="fd218-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="fd218-243">j.</span><span class="sxs-lookup"><span data-stu-id="fd218-243">j.</span></span> <span data-ttu-id="fd218-244">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fd218-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="fd218-245">Puede usar cualquier otra Picturepark usuario cuenta herramienta de creación o las API proporcionadas por Picturepark tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd218-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fd218-246">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd218-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fd218-247">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPicturepark.</span><span class="sxs-lookup"><span data-stu-id="fd218-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fd218-249">**tooassign Britta Simon tooPicturepark, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fd218-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd218-250">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fd218-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fd218-252">En la lista de aplicaciones de hello, seleccione **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="fd218-252">In hello applications list, select **Picturepark**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="fd218-254">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fd218-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fd218-256">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fd218-256">Click **Add** button.</span></span> <span data-ttu-id="fd218-257">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fd218-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fd218-259">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd218-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fd218-260">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fd218-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd218-261">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fd218-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd218-262">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fd218-262">Testing single sign-on</span></span>

<span data-ttu-id="fd218-263">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fd218-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fd218-264">Al hacer clic en icono de Picturepark Hola Hola Panel de acceso, deberá obtener aplicaciones de Picturepark tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="fd218-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="fd218-265">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fd218-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd218-266">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fd218-266">Additional resources</span></span>

* [<span data-ttu-id="fd218-267">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd218-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd218-268">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fd218-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

