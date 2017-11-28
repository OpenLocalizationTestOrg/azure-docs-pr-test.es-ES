---
title: "Tutorial: Integración de Azure Active Directory con Zoom | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el Zoom."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="4b0e4-103">Tutorial: Integración de Azure Active Directory con Zoom</span><span class="sxs-lookup"><span data-stu-id="4b0e4-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="4b0e4-104">En este tutorial, aprenderá cómo toointegrate Zoom con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b0e4-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b0e4-105">Integración de Zoom con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b0e4-106">Puede controlar en Azure AD que tenga acceso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="4b0e4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZoom (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4b0e4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4b0e4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b0e4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b0e4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4b0e4-110">Prerequisites</span></span>

<span data-ttu-id="4b0e4-111">integración de Azure AD tooconfigure con Zoom, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="4b0e4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b0e4-113">Una suscripción habilitada para el inicio de sesión único en Zoo</span><span class="sxs-lookup"><span data-stu-id="4b0e4-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b0e4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b0e4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b0e4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b0e4-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b0e4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b0e4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4b0e4-118">Scenario description</span></span>
<span data-ttu-id="4b0e4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b0e4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b0e4-121">Adición de Zoom de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4b0e4-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="4b0e4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="4b0e4-123">Adición de Zoom de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4b0e4-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="4b0e4-124">integración de hello tooconfigure de Zoom en Azure AD, deberá tooadd Zoom de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b0e4-125">**tooadd Zoom de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b0e4-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0e4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="4b0e4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b0e4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="4b0e4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="4b0e4-133">En el cuadro de búsqueda de hello, escriba **Zoom**, seleccione **Zoom** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Zoom en la lista de resultados de Hola](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4b0e4-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0e4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4b0e4-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Zoom con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4b0e4-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b0e4-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zoom es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="4b0e4-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zoom necesidades toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="4b0e4-139">En Zoom, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b0e4-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Zoom, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b0e4-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b0e4-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b0e4-143">**[Crear un usuario de prueba de Zoom](#create-a-zoom-test-user)**  -toohave un equivalente de Britta Simon en Zoom que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b0e4-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b0e4-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4b0e4-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0e4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4b0e4-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zoom.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="4b0e4-148">**tooconfigure inicio de sesión único en Azure AD con Zoom, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b0e4-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0e4-149">En el portal de Azure, en Hola Hola **Zoom** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="4b0e4-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="4b0e4-153">En hello **Zoom dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="4b0e4-155">a.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-155">a.</span></span> <span data-ttu-id="4b0e4-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="4b0e4-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="4b0e4-157">b.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-157">b.</span></span> <span data-ttu-id="4b0e4-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="4b0e4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b0e4-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-159">These values are not real.</span></span> <span data-ttu-id="4b0e4-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4b0e4-161">Póngase en contacto con [equipo de soporte técnico de Zoom cliente](https://support.zoom.us/hc) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="4b0e4-162">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="4b0e4-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4b0e4-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b0e4-166">En hello **configuración Zoom** sección, haga clic en **configurar Zoom** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4b0e4-167">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="4b0e4-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="4b0e4-169">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de Zoom de tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="4b0e4-170">Haga clic en hello **Single Sign-On** ficha.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="4b0e4-171">![Pestaña de Inicio de sesión único](./media/active-directory-saas-zoom-tutorial/IC784700.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4b0e4-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="4b0e4-172">Haga clic en hello **Control de seguridad** ficha y, a continuación, vaya a toohello **Single Sign-On** configuración.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="4b0e4-173">Hola sección Single Sign-On, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4b0e4-174">![Sección de Inicio de sesión único](./media/active-directory-saas-zoom-tutorial/IC784701.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4b0e4-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="4b0e4-175">a.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-175">a.</span></span> <span data-ttu-id="4b0e4-176">Hola **URL de la página de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="4b0e4-177">b.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-177">b.</span></span> <span data-ttu-id="4b0e4-178">Hola **URL de la página de cierre de sesión** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="4b0e4-179">c.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-179">c.</span></span> <span data-ttu-id="4b0e4-180">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="4b0e4-181">d.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-181">d.</span></span> <span data-ttu-id="4b0e4-182">Hola **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4b0e4-183">e.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-183">e.</span></span> <span data-ttu-id="4b0e4-184">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4b0e4-185">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4b0e4-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b0e4-186">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b0e4-187">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b0e4-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4b0e4-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0e4-188">Create an Azure AD test user</span></span>

<span data-ttu-id="4b0e4-189">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="4b0e4-191">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b0e4-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0e4-192">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4b0e4-194">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4b0e4-196">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4b0e4-198">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4b0e4-200">a.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-200">a.</span></span> <span data-ttu-id="4b0e4-201">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b0e4-202">b.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-202">b.</span></span> <span data-ttu-id="4b0e4-203">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4b0e4-204">c.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-204">c.</span></span> <span data-ttu-id="4b0e4-205">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4b0e4-206">d.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-206">d.</span></span> <span data-ttu-id="4b0e4-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="4b0e4-208">Crear un usuario de prueba de Zoom</span><span class="sxs-lookup"><span data-stu-id="4b0e4-208">Create a Zoom test user</span></span>

<span data-ttu-id="4b0e4-209">En orden tooenable Azure AD a los usuarios toolog en tooZoom, se les deben aprovisionar en Zoom.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="4b0e4-210">En caso de hello de Zoom, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="4b0e4-211">tooprovision una cuenta de usuario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="4b0e4-212">Inicie sesión en tooyour **Zoom** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="4b0e4-213">Haga clic en hello **administración de cuentas** ficha y, a continuación, haga clic en **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="4b0e4-214">En la sección de administración de usuarios de hello, haga clic en **agregar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="4b0e4-215">![Administración de usuarios](./media/active-directory-saas-zoom-tutorial/IC784703.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="4b0e4-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="4b0e4-216">En hello **agregar usuarios** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4b0e4-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="4b0e4-217">![Agregar usuarios](./media/active-directory-saas-zoom-tutorial/IC784704.png "Agregar usuarios")</span><span class="sxs-lookup"><span data-stu-id="4b0e4-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="4b0e4-218">a.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-218">a.</span></span> <span data-ttu-id="4b0e4-219">Como **Tipo de usuario**, seleccione **Básico**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="4b0e4-220">b.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-220">b.</span></span> <span data-ttu-id="4b0e4-221">Hola **mensajes de correo electrónico** cuadro de texto, dirección de correo electrónico de tipo hello de un Azure válida que desee tooprovision de cuenta de AD.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="4b0e4-222">c.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-222">c.</span></span> <span data-ttu-id="4b0e4-223">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="4b0e4-224">Puede usar cualquier otra Zoom usuario cuenta herramienta de creación o las API proporcionadas por Zoom tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4b0e4-225">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0e4-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4b0e4-226">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="4b0e4-228">**tooassign Britta Simon tooZoom, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b0e4-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0e4-229">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4b0e4-231">En la lista de aplicaciones de hello, seleccione **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-231">In hello applications list, select **Zoom**.</span></span>

    ![vínculo de Zoom de Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="4b0e4-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="4b0e4-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-235">Click **Add** button.</span></span> <span data-ttu-id="4b0e4-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="4b0e4-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b0e4-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b0e4-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4b0e4-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="4b0e4-241">Test single sign-on</span></span>

<span data-ttu-id="4b0e4-242">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b0e4-243">Al hacer clic en icono de Zoom de Hola Hola Panel de acceso, deberá obtener aplicaciones de Zoom tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="4b0e4-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b0e4-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4b0e4-244">Additional resources</span></span>

* [<span data-ttu-id="4b0e4-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b0e4-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b0e4-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b0e4-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

