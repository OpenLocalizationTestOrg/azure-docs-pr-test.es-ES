---
title: "Tutorial: Integración de Azure Active Directory con Image Relay | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la retransmisión de imagen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="e1d06-103">Tutorial: Integración de Azure Active Directory con Image Relay</span><span class="sxs-lookup"><span data-stu-id="e1d06-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="e1d06-104">En este tutorial, aprenderá cómo toointegrate retransmisión de imagen con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1d06-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1d06-105">Integración de retransmisión de imagen con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e1d06-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1d06-106">Puede controlar en Azure AD que tenga acceso tooImage retransmisión</span><span class="sxs-lookup"><span data-stu-id="e1d06-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="e1d06-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooImage retransmisión (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d06-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1d06-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e1d06-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1d06-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1d06-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1d06-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e1d06-110">Prerequisites</span></span>

<span data-ttu-id="e1d06-111">tooconfigure integración de Azure AD con retransmisión de imagen, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e1d06-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="e1d06-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d06-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1d06-113">Una suscripción habilitada para inicio de sesión único en Image Relay</span><span class="sxs-lookup"><span data-stu-id="e1d06-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1d06-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e1d06-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1d06-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e1d06-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1d06-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e1d06-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1d06-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1d06-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1d06-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e1d06-118">Scenario description</span></span>
<span data-ttu-id="e1d06-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e1d06-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1d06-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e1d06-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1d06-121">Agregar imagen de retransmisión de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e1d06-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="e1d06-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d06-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="e1d06-123">Agregar imagen de retransmisión de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e1d06-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="e1d06-124">integración de hello tooconfigure de retransmisión de imagen en Azure AD, deberá tooadd retransmisión de imagen de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e1d06-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1d06-125">**tooadd retransmisión de imagen de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1d06-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d06-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e1d06-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1d06-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1d06-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e1d06-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1d06-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e1d06-133">En el cuadro de búsqueda de hello, escriba **imagen retransmisión**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-133">In hello search box, type **Image Relay**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="e1d06-135">En el panel de resultados de hello, seleccione **imagen retransmisión**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e1d06-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1d06-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d06-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1d06-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Image Relay con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e1d06-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1d06-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en retransmisión de imagen es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1d06-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="e1d06-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en retransmisión de imagen debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e1d06-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="e1d06-141">En la retransmisión de imagen, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1d06-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e1d06-142">tooconfigure y prueba de inicio de sesión único en Azure AD con retransmisión de imagen, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e1d06-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1d06-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e1d06-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1d06-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1d06-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1d06-145">**[Creación de un usuario de prueba de retransmisión de imagen](#creating-an-image-relay-test-user)**  -toohave un equivalente de Britta Simon en retransmisión de imagen que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="e1d06-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1d06-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e1d06-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1d06-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e1d06-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1d06-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d06-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1d06-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de retransmisión de imagen.</span><span class="sxs-lookup"><span data-stu-id="e1d06-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="e1d06-150">**inicio de sesión único en tooconfigure Azure AD con retransmisión de imagen, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1d06-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d06-151">En el portal de Azure, en Hola Hola **imagen retransmisión** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e1d06-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e1d06-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="e1d06-155">En hello **dominio de retransmisión de imagen y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e1d06-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="e1d06-157">a.</span><span class="sxs-lookup"><span data-stu-id="e1d06-157">a.</span></span> <span data-ttu-id="e1d06-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="e1d06-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="e1d06-159">b.</span><span class="sxs-lookup"><span data-stu-id="e1d06-159">b.</span></span> <span data-ttu-id="e1d06-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="e1d06-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1d06-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e1d06-161">These values are not real.</span></span> <span data-ttu-id="e1d06-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="e1d06-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e1d06-163">Póngase en contacto con [equipo de soporte técnico de cliente de retransmisión de imagen](http://support.imagerelay.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="e1d06-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="e1d06-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e1d06-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="e1d06-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e1d06-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1d06-168">En hello **configuración de retransmisión de imagen** sección, haga clic en **configurar imagen retransmisión** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="e1d06-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1d06-169">Hola copia **dirección URL del servicio de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="e1d06-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="e1d06-171">En otra ventana del explorador, inicie sesión en el sitio de empresa de retransmisión de imagen tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="e1d06-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="e1d06-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en hello **usuarios y permisos** carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e1d06-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="e1d06-174">Haga clic en **Create New Permission**(Crear permiso nuevo).</span><span class="sxs-lookup"><span data-stu-id="e1d06-174">Click **Create New Permission**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="e1d06-176">Hola **inicio de sesión único en la configuración** carga de trabajo, seleccione hello **este grupo puede solo iniciar sesión mediante el inicio de sesión único** casilla de verificación y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="e1d06-178">Vaya demasiado**configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-178">Go too**Account Settings**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="e1d06-180">Vaya toohello **inicio de sesión único en la configuración** carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e1d06-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="e1d06-182">En hello **configuración SAML** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e1d06-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="e1d06-184">a.</span><span class="sxs-lookup"><span data-stu-id="e1d06-184">a.</span></span> <span data-ttu-id="e1d06-185">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d06-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1d06-186">b.</span><span class="sxs-lookup"><span data-stu-id="e1d06-186">b.</span></span> <span data-ttu-id="e1d06-187">En **Logout URL** cuadro de texto, pegue Hola valo **dirección URL del servicio de cierre de sesión único** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d06-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1d06-188">c.</span><span class="sxs-lookup"><span data-stu-id="e1d06-188">c.</span></span> <span data-ttu-id="e1d06-189">En **Name Id Format** (Formato de id. de nombre), seleccione **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="e1d06-190">d.</span><span class="sxs-lookup"><span data-stu-id="e1d06-190">d.</span></span> <span data-ttu-id="e1d06-191">Como **opciones de enlace para las solicitudes de hello (imagen retransmisión) del proveedor de servicios**, seleccione **enlace POST**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="e1d06-192">e.</span><span class="sxs-lookup"><span data-stu-id="e1d06-192">e.</span></span> <span data-ttu-id="e1d06-193">En **x.509 Certificate** (Certificado x.509), haga clic en **Update Certificate** (Actualizar certificado).</span><span class="sxs-lookup"><span data-stu-id="e1d06-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="e1d06-195">f.</span><span class="sxs-lookup"><span data-stu-id="e1d06-195">f.</span></span> <span data-ttu-id="e1d06-196">Abra el certificado de hello descargado en el Bloc de notas, copie el contenido de hello y, a continuación, péguelo en el cuadro de texto de hello x.509 certificado.</span><span class="sxs-lookup"><span data-stu-id="e1d06-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="e1d06-198">g.</span><span class="sxs-lookup"><span data-stu-id="e1d06-198">g.</span></span> <span data-ttu-id="e1d06-199">En **Just el aprovisionamiento de usuarios** sección, seleccione hello **habilitar el aprovisionamiento de usuarios Just**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="e1d06-201">h.</span><span class="sxs-lookup"><span data-stu-id="e1d06-201">h.</span></span> <span data-ttu-id="e1d06-202">Grupo de permisos SELECT hello (por ejemplo, **SSO básica**) que se permite toosign en sólo a través de un inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e1d06-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="e1d06-204">i.</span><span class="sxs-lookup"><span data-stu-id="e1d06-204">i.</span></span> <span data-ttu-id="e1d06-205">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e1d06-206">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e1d06-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1d06-207">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e1d06-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1d06-208">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1d06-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1d06-209">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d06-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1d06-210">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e1d06-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e1d06-212">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1d06-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d06-213">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e1d06-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1d06-215">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1d06-217">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1d06-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1d06-219">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e1d06-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1d06-221">a.</span><span class="sxs-lookup"><span data-stu-id="e1d06-221">a.</span></span> <span data-ttu-id="e1d06-222">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1d06-223">b.</span><span class="sxs-lookup"><span data-stu-id="e1d06-223">b.</span></span> <span data-ttu-id="e1d06-224">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e1d06-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1d06-225">c.</span><span class="sxs-lookup"><span data-stu-id="e1d06-225">c.</span></span> <span data-ttu-id="e1d06-226">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1d06-227">d.</span><span class="sxs-lookup"><span data-stu-id="e1d06-227">d.</span></span> <span data-ttu-id="e1d06-228">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="e1d06-229">Creación de un usuario de prueba de Image Relay</span><span class="sxs-lookup"><span data-stu-id="e1d06-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="e1d06-230">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en retransmisión de imagen.</span><span class="sxs-lookup"><span data-stu-id="e1d06-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="e1d06-231">**toocreate un usuario llamado Britta Simon en retransmisión de imagen, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1d06-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d06-232">Sitio de empresa de retransmisión de imagen tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="e1d06-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="e1d06-233">Vaya demasiado**usuarios y permisos** y seleccione **Create User de SSO**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="e1d06-235">Escriba hello **correo electrónico**, **nombre**, **Last Name**, y **empresa** del usuario de hello desea tooprovision y grupo de permisos select Hola (por ejemplo, SSO básica) que es el grupo de Hola que puede iniciar sesión en solo a través de un inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e1d06-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="e1d06-237">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1d06-238">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d06-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e1d06-239">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooImage retransmisión.</span><span class="sxs-lookup"><span data-stu-id="e1d06-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e1d06-241">**tooassign Britta Simon tooImage retransmisión, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1d06-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d06-242">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e1d06-244">En la lista de aplicaciones de hello, seleccione **imagen retransmisión**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-244">In hello applications list, select **Image Relay**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="e1d06-246">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e1d06-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-248">Click **Add** button.</span></span> <span data-ttu-id="e1d06-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e1d06-251">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1d06-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1d06-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1d06-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e1d06-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1d06-254">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e1d06-254">Testing single sign-on</span></span>

<span data-ttu-id="e1d06-255">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e1d06-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="e1d06-256">Al hacer clic en icono de imagen retransmisión Hola Hola Panel de acceso, deberá obtener la aplicación de imagen retransmisión tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="e1d06-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e1d06-257">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e1d06-257">Additional resources</span></span>

* [<span data-ttu-id="e1d06-258">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1d06-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1d06-259">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1d06-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

