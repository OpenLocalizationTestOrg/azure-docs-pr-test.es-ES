---
title: "Tutorial: Integración de Azure Active Directory con Front | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la parte delantera."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="aba41-103">Tutorial: integración de Azure Active Directory con Front</span><span class="sxs-lookup"><span data-stu-id="aba41-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="aba41-104">En este tutorial, aprenderá cómo toointegrate frontal con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aba41-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aba41-105">Integración frontal con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="aba41-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aba41-106">Puede controlar en Azure AD que tenga acceso tooFront.</span><span class="sxs-lookup"><span data-stu-id="aba41-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="aba41-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFront (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aba41-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="aba41-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="aba41-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="aba41-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aba41-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aba41-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aba41-110">Prerequisites</span></span>

<span data-ttu-id="aba41-111">integración de tooconfigure Azure AD con la parte delantera, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="aba41-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="aba41-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aba41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aba41-113">Una suscripción habilitada para el inicio de sesión único en Front</span><span class="sxs-lookup"><span data-stu-id="aba41-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aba41-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="aba41-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aba41-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="aba41-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aba41-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aba41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aba41-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aba41-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aba41-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="aba41-118">Scenario description</span></span>
<span data-ttu-id="aba41-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="aba41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aba41-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="aba41-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aba41-121">Agregar parte delantera de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aba41-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="aba41-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aba41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="aba41-123">Agregar parte delantera de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aba41-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="aba41-124">integración de hello tooconfigure del principio en Azure AD, deberá tooadd frontal de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="aba41-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aba41-125">**tooadd parte delantera de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aba41-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aba41-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="aba41-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="aba41-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="aba41-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aba41-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aba41-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="aba41-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aba41-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="aba41-133">En el cuadro de búsqueda de hello, escriba **front-**, seleccione **front-** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aba41-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de la parte delantera de Hola](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="aba41-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="aba41-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="aba41-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Front con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aba41-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aba41-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario de hello equivalente en la parte frontal es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aba41-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="aba41-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y Hola de usuario en la parte delantera debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="aba41-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="aba41-139">En la parte delantera, asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aba41-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aba41-140">tooconfigure y prueba de inicio de sesión único en Azure AD con frontal, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="aba41-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aba41-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="aba41-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aba41-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aba41-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aba41-143">**[Crear un usuario de prueba de la parte delantera](#create-a-front-test-user)**  -toohave un equivalente de Britta Simon en primer plano que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="aba41-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aba41-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aba41-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aba41-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="aba41-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="aba41-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aba41-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="aba41-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de principio.</span><span class="sxs-lookup"><span data-stu-id="aba41-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="aba41-148">**tooconfigure inicio de sesión único en Azure AD con frente, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aba41-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="aba41-149">En el portal de Azure, en Hola Hola **front-** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="aba41-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="aba41-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aba41-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="aba41-153">En hello **front-dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="aba41-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="aba41-155">a.</span><span class="sxs-lookup"><span data-stu-id="aba41-155">a.</span></span> <span data-ttu-id="aba41-156">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="aba41-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="aba41-157">b.</span><span class="sxs-lookup"><span data-stu-id="aba41-157">b.</span></span> <span data-ttu-id="aba41-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="aba41-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="aba41-159">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="aba41-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="aba41-161">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="aba41-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="aba41-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="aba41-162">These values are not real.</span></span> <span data-ttu-id="aba41-163">Actualización de estos valores con Hola real identificador, dirección URL de respuesta y dirección URL de inicio de sesión que se describen más adelante en el tutorial o póngase en contacto con [equipo de soporte técnico de cliente front-](mailto:support@frontapp.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="aba41-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="aba41-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="aba41-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="aba41-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="aba41-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="aba41-168">En hello **configuración front-** sección, haga clic en **configurar front-** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="aba41-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aba41-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="aba41-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="aba41-171">Inquilino de principio tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="aba41-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="aba41-172">Vaya demasiado**configuración (icono de engranaje final Hola de barra lateral izquierdo de hello) > Preferencias**.</span><span class="sxs-lookup"><span data-stu-id="aba41-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="aba41-174">Haga clic en el vínculo **Inicio de sesión único** .</span><span class="sxs-lookup"><span data-stu-id="aba41-174">Click **Single Sign On** link.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="aba41-176">Seleccione **SAML** en la lista desplegable de Hola de **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="aba41-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="aba41-178">Hola **punto de entrada** textbox coloca el valor de Hola de **URL de servicio de inicio de sesión único** desde el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aba41-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="aba41-180">Abra su descargado **Certificate(Base64)** un archivo en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado de firma de** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="aba41-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="aba41-182">En hello **configuración del proveedor de servicio** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="aba41-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="aba41-184">a.</span><span class="sxs-lookup"><span data-stu-id="aba41-184">a.</span></span> <span data-ttu-id="aba41-185">Copiar valor de Hola de **Id. de entidad** y péguelo en hello **identificador** en el cuadro de texto **front-dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="aba41-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="aba41-186">b.</span><span class="sxs-lookup"><span data-stu-id="aba41-186">b.</span></span> <span data-ttu-id="aba41-187">Copiar valor de Hola de **dirección URL de ACS** y péguelo en hello **dirección URL de inicio de sesión** en el cuadro de texto **front-dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="aba41-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="aba41-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="aba41-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="aba41-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="aba41-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aba41-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="aba41-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aba41-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aba41-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="aba41-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aba41-192">Create an Azure AD test user</span></span>

<span data-ttu-id="aba41-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="aba41-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="aba41-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aba41-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aba41-196">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="aba41-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="aba41-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="aba41-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="aba41-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aba41-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="aba41-202">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="aba41-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="aba41-204">a.</span><span class="sxs-lookup"><span data-stu-id="aba41-204">a.</span></span> <span data-ttu-id="aba41-205">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aba41-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aba41-206">b.</span><span class="sxs-lookup"><span data-stu-id="aba41-206">b.</span></span> <span data-ttu-id="aba41-207">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aba41-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="aba41-208">c.</span><span class="sxs-lookup"><span data-stu-id="aba41-208">c.</span></span> <span data-ttu-id="aba41-209">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="aba41-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="aba41-210">d.</span><span class="sxs-lookup"><span data-stu-id="aba41-210">d.</span></span> <span data-ttu-id="aba41-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="aba41-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="aba41-212">Creación de un usuario de prueba de Front</span><span class="sxs-lookup"><span data-stu-id="aba41-212">Create a Front test user</span></span>

<span data-ttu-id="aba41-213">En esta sección, creará un usuario llamado Britta Simon en Front.</span><span class="sxs-lookup"><span data-stu-id="aba41-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="aba41-214">Trabajar con [equipo de soporte técnico de cliente front-](mailto:support@frontapp.com) para agregar usuarios de hello en la plataforma de la parte delantera de Hola.</span><span class="sxs-lookup"><span data-stu-id="aba41-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="aba41-215">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aba41-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="aba41-216">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aba41-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="aba41-217">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooFront.</span><span class="sxs-lookup"><span data-stu-id="aba41-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="aba41-219">**tooassign Britta Simon tooFront, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aba41-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="aba41-220">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aba41-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="aba41-222">En la lista de aplicaciones de hello, seleccione **front-**.</span><span class="sxs-lookup"><span data-stu-id="aba41-222">In hello applications list, select **Front**.</span></span>

    ![vínculo de principio Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="aba41-224">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aba41-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="aba41-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="aba41-226">Click **Add** button.</span></span> <span data-ttu-id="aba41-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aba41-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="aba41-229">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="aba41-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aba41-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aba41-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aba41-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aba41-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="aba41-232">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="aba41-232">Test single sign-on</span></span>

<span data-ttu-id="aba41-233">objetivo de Hola de esta sección es tootest el uso de Azure AD SSOconfiguration Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="aba41-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="aba41-234">Al hacer clic en icono de principio Hola Hola Panel de acceso, deberá obtener la aplicación de principio tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="aba41-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aba41-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="aba41-235">Additional resources</span></span>

* [<span data-ttu-id="aba41-236">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aba41-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aba41-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aba41-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

