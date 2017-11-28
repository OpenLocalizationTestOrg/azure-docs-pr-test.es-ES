---
title: "Tutorial: integración de Azure Active Directory con Recognize | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y reconocer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="32297-103">Tutorial: Integración de Azure Active Directory con Recognize</span><span class="sxs-lookup"><span data-stu-id="32297-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="32297-104">En este tutorial, aprenderá cómo reconocer toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32297-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32297-105">Reconocer la integración con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="32297-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32297-106">Puede controlar en Azure AD que tenga acceso tooRecognize</span><span class="sxs-lookup"><span data-stu-id="32297-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="32297-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRecognize (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32297-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32297-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="32297-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32297-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32297-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32297-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="32297-110">Prerequisites</span></span>

<span data-ttu-id="32297-111">integración de Azure AD tooconfigure con reconocer, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="32297-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="32297-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32297-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32297-113">Una suscripción habilitada para el inicio de sesión único en Recognize</span><span class="sxs-lookup"><span data-stu-id="32297-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32297-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="32297-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32297-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="32297-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32297-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="32297-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32297-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32297-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32297-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="32297-118">Scenario description</span></span>
<span data-ttu-id="32297-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="32297-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32297-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="32297-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32297-121">Agregar reconocer desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="32297-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="32297-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32297-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="32297-123">Agregar reconocer desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="32297-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="32297-124">integración de hello tooconfigure de reconocer en Azure AD, deberá tooadd reconocer de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="32297-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32297-125">**tooadd reconocer desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32297-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32297-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="32297-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32297-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="32297-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32297-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="32297-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="32297-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32297-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="32297-133">En el cuadro de búsqueda de hello, escriba **reconocer**.</span><span class="sxs-lookup"><span data-stu-id="32297-133">In hello search box, type **Recognize**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="32297-135">En el panel de resultados de hello, seleccione **reconocer**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="32297-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32297-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32297-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32297-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Recognize con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32297-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32297-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en reconocer es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32297-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="32297-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en reconocer debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="32297-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="32297-141">En reconocer, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32297-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="32297-142">prueba Azure AD y tooconfigure inicio de sesión único con reconocer, necesita hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="32297-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32297-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="32297-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32297-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32297-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32297-145">**[Crear un usuario de prueba de reconocer](#creating-a-recognize-test-user)**  -toohave un equivalente de Britta Simon en reconocer que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="32297-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32297-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="32297-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32297-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="32297-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32297-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32297-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32297-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de reconocer.</span><span class="sxs-lookup"><span data-stu-id="32297-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="32297-150">**inicio de sesión único en Azure AD tooconfigure con reconocer, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32297-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="32297-151">En el portal de Azure, en Hola Hola **reconocer** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="32297-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="32297-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="32297-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="32297-155">En hello **reconocer dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="32297-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="32297-157">a.</span><span class="sxs-lookup"><span data-stu-id="32297-157">a.</span></span> <span data-ttu-id="32297-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="32297-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="32297-159">b.</span><span class="sxs-lookup"><span data-stu-id="32297-159">b.</span></span> <span data-ttu-id="32297-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="32297-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32297-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="32297-161">These values are not real.</span></span> <span data-ttu-id="32297-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="32297-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32297-163">Póngase en contacto con [equipo de soporte técnico de cliente reconoce](mailto:support@recognizeapp.com) obtener la dirección URL de inicio de sesión y puede obtener el valor de identificador abriendo Hola dirección URL de metadatos del proveedor de servicio de la sección de configuración de SSO que se explica más adelante en el tutorial Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="32297-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="32297-164">.</span><span class="sxs-lookup"><span data-stu-id="32297-164">.</span></span> 
 
4. <span data-ttu-id="32297-165">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="32297-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="32297-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="32297-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32297-169">En hello **reconocer configuración** sección, haga clic en **configurar reconocer** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="32297-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="32297-170">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="32297-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="32297-172">En una ventana del explorador web diferente, inicio de sesión tooyour reconocer inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="32297-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="32297-173">En hello esquina superior derecha, haga clic en **menú**.</span><span class="sxs-lookup"><span data-stu-id="32297-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="32297-174">Vaya demasiado**Administrador de la compañía**.</span><span class="sxs-lookup"><span data-stu-id="32297-174">Go too**Company Admin**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="32297-176">En el panel de navegación izquierdo de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="32297-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="32297-178">Realizar Hola seguir pasos de **configuración de SSO** sección.</span><span class="sxs-lookup"><span data-stu-id="32297-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="32297-180">a.</span><span class="sxs-lookup"><span data-stu-id="32297-180">a.</span></span> <span data-ttu-id="32297-181">En **Enable SSO** (Habilitar SSO), seleccione **ON** (Activado).</span><span class="sxs-lookup"><span data-stu-id="32297-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="32297-182">b.</span><span class="sxs-lookup"><span data-stu-id="32297-182">b.</span></span> <span data-ttu-id="32297-183">Hola **Id. de entidad IDP** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="32297-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="32297-184">c.</span><span class="sxs-lookup"><span data-stu-id="32297-184">c.</span></span> <span data-ttu-id="32297-185">Hola **dirección url de destino de Sso** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="32297-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="32297-186">d.</span><span class="sxs-lookup"><span data-stu-id="32297-186">d.</span></span> <span data-ttu-id="32297-187">Hola **dirección url de destino de Slo** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="32297-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="32297-188">e.</span><span class="sxs-lookup"><span data-stu-id="32297-188">e.</span></span> <span data-ttu-id="32297-189">Abra su descargado **certificado (Base64)** un archivo en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="32297-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="32297-190">f.</span><span class="sxs-lookup"><span data-stu-id="32297-190">f.</span></span> <span data-ttu-id="32297-191">Haga clic en hello **Guardar configuración** botón.</span><span class="sxs-lookup"><span data-stu-id="32297-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="32297-192">Al lado de hello **configuración de SSO** sección, copie la dirección URL de hello en **dirección url de metadatos del proveedor de servicio**.</span><span class="sxs-lookup"><span data-stu-id="32297-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="32297-194">Abra hello **vínculo de dirección URL de metadatos** en un documento de metadatos en blanco del explorador toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="32297-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="32297-195">A continuación, copie Hola EntityDescriptor value(entityID) archivo hello y péguelo en **identificador** en el cuadro de texto **sección reconocer dominio y las direcciones URL** en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="32297-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="32297-197">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="32297-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32297-198">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="32297-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32297-199">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32297-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32297-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32297-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="32297-201">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="32297-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="32297-203">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32297-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32297-204">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="32297-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32297-206">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="32297-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32297-208">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32297-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32297-210">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="32297-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32297-212">a.</span><span class="sxs-lookup"><span data-stu-id="32297-212">a.</span></span> <span data-ttu-id="32297-213">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32297-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32297-214">b.</span><span class="sxs-lookup"><span data-stu-id="32297-214">b.</span></span> <span data-ttu-id="32297-215">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32297-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32297-216">c.</span><span class="sxs-lookup"><span data-stu-id="32297-216">c.</span></span> <span data-ttu-id="32297-217">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="32297-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32297-218">d.</span><span class="sxs-lookup"><span data-stu-id="32297-218">d.</span></span> <span data-ttu-id="32297-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="32297-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="32297-220">Creación de un usuario de prueba de Recognize</span><span class="sxs-lookup"><span data-stu-id="32297-220">Creating a Recognize test user</span></span>

<span data-ttu-id="32297-221">En orden tooenable toolog de los usuarios de Azure AD en reconocer, se les deben aprovisionar en reconocer.</span><span class="sxs-lookup"><span data-stu-id="32297-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="32297-222">En caso de hello de reconocer, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="32297-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="32297-223">Esta aplicación no admite el aprovisionamiento SCIM, pero tiene una sincronización de usuario alternativa que aprovisiona a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="32297-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="32297-224">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32297-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="32297-225">Inicie sesión en su sitio de la compañía de Recognize como administrador.</span><span class="sxs-lookup"><span data-stu-id="32297-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="32297-226">En hello esquina superior derecha, haga clic en **menú**.</span><span class="sxs-lookup"><span data-stu-id="32297-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="32297-227">Vaya demasiado**Administrador de la compañía**.</span><span class="sxs-lookup"><span data-stu-id="32297-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="32297-228">En el panel de navegación izquierdo de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="32297-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="32297-229">Realizar Hola seguir pasos de **usuario sincronización** sección.</span><span class="sxs-lookup"><span data-stu-id="32297-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="32297-230">![Nuevo usuario](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="32297-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="32297-231">a.</span><span class="sxs-lookup"><span data-stu-id="32297-231">a.</span></span> <span data-ttu-id="32297-232">En **Sync Enabled** (Sincronización habilitada), seleccione **ON** (Activado).</span><span class="sxs-lookup"><span data-stu-id="32297-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="32297-233">b.</span><span class="sxs-lookup"><span data-stu-id="32297-233">b.</span></span> <span data-ttu-id="32297-234">En **Choose sync provider** (Elegir proveedor de sincronización), seleccione **Microsoft/Office 365**.</span><span class="sxs-lookup"><span data-stu-id="32297-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="32297-235">c.</span><span class="sxs-lookup"><span data-stu-id="32297-235">c.</span></span> <span data-ttu-id="32297-236">Haga clic en **Run User Sync** (Ejecutar sincronización de usuario).</span><span class="sxs-lookup"><span data-stu-id="32297-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32297-237">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="32297-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32297-238">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRecognize.</span><span class="sxs-lookup"><span data-stu-id="32297-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="32297-240">**tooassign Britta Simon tooRecognize, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32297-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="32297-241">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="32297-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="32297-243">En la lista de aplicaciones de hello, seleccione **reconocer**.</span><span class="sxs-lookup"><span data-stu-id="32297-243">In hello applications list, select **Recognize**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="32297-245">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="32297-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="32297-247">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="32297-247">Click **Add** button.</span></span> <span data-ttu-id="32297-248">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="32297-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="32297-250">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="32297-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32297-251">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="32297-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32297-252">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="32297-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32297-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="32297-253">Testing single sign-on</span></span>

<span data-ttu-id="32297-254">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="32297-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="32297-255">Al hacer clic en icono de reconocer Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour reconocer aplicación.</span><span class="sxs-lookup"><span data-stu-id="32297-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="32297-256">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32297-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32297-257">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="32297-257">Additional resources</span></span>

* [<span data-ttu-id="32297-258">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32297-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32297-259">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32297-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

