---
title: "Tutorial: Integración de Azure Active Directory con Halogen Software | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el Software de halógeno."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="629ca-103">Tutorial: Integración de Azure Active Directory con Halogen Software</span><span class="sxs-lookup"><span data-stu-id="629ca-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="629ca-104">En este tutorial, aprenderá cómo toointegrate halógeno Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="629ca-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="629ca-105">La integración del Software de halógeno con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="629ca-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="629ca-106">Puede controlar en Azure AD que tenga acceso tooHalogen Software</span><span class="sxs-lookup"><span data-stu-id="629ca-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="629ca-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHalogen Software (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ca-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="629ca-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="629ca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="629ca-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="629ca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="629ca-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="629ca-110">Prerequisites</span></span>

<span data-ttu-id="629ca-111">integración de Azure AD con Software halógenas tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="629ca-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="629ca-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="629ca-113">Un suscripción habilitada para el inicio de sesión único en Halogen Software</span><span class="sxs-lookup"><span data-stu-id="629ca-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="629ca-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="629ca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="629ca-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="629ca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="629ca-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="629ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="629ca-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="629ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="629ca-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="629ca-118">Scenario description</span></span>

<span data-ttu-id="629ca-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="629ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="629ca-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="629ca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="629ca-121">Agregar Software halógeno desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="629ca-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="629ca-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="629ca-123">Agregar Software halógeno desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="629ca-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="629ca-124">integración de hello tooconfigure del Software de halógeno en Azure AD, deberá tooadd Software halógenas de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="629ca-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="629ca-125">**tooadd Software halógenas de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="629ca-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="629ca-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="629ca-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="629ca-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="629ca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="629ca-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="629ca-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="629ca-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="629ca-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="629ca-133">En el cuadro de búsqueda de hello, escriba **Software halógenas**.</span><span class="sxs-lookup"><span data-stu-id="629ca-133">In hello search box, type **Halogen Software**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="629ca-135">En el panel de resultados de hello, seleccione **Software halógenas**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="629ca-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="629ca-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="629ca-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Halogen Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="629ca-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="629ca-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Software halógeno es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629ca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="629ca-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Software halógeno debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="629ca-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="629ca-141">En Software halógenas, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="629ca-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="629ca-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Software halógenas, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="629ca-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="629ca-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="629ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="629ca-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="629ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="629ca-145">**[Crear un usuario de prueba de Software halógenas](#creating-a-halogen-software-test-user)**  -toohave un equivalente de Britta Simon en Software halógeno representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="629ca-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="629ca-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="629ca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="629ca-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="629ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="629ca-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="629ca-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Software de halógeno.</span><span class="sxs-lookup"><span data-stu-id="629ca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="629ca-150">**Azure AD tooconfigure inicio de sesión único con el Software de halógeno, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="629ca-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="629ca-151">En el portal de Azure, en Hola Hola **Software halógenas** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="629ca-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="629ca-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="629ca-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="629ca-155">En hello **halógeno Software dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="629ca-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="629ca-157">a.</span><span class="sxs-lookup"><span data-stu-id="629ca-157">a.</span></span> <span data-ttu-id="629ca-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="629ca-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="629ca-159">b.</span><span class="sxs-lookup"><span data-stu-id="629ca-159">b.</span></span> <span data-ttu-id="629ca-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="629ca-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="629ca-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="629ca-161">These values are not real.</span></span> <span data-ttu-id="629ca-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="629ca-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="629ca-163">Póngase en contacto con [equipo de soporte técnico de cliente de Software halógenas](https://support.halogensoftware.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="629ca-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="629ca-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="629ca-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="629ca-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="629ca-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="629ca-168">En otra ventana del explorador, inicio de sesión tooyour **Software halógenas** aplicación como administrador.</span><span class="sxs-lookup"><span data-stu-id="629ca-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="629ca-169">Haga clic en hello **opciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="629ca-169">Click hello **Options** tab.</span></span> 
   
    ![Qué es Azure AD Connect][12]

8. <span data-ttu-id="629ca-171">En el panel de navegación izquierdo de hello, haga clic en **configuración de SAML**.</span><span class="sxs-lookup"><span data-stu-id="629ca-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Qué es Azure AD Connect][13]

9. <span data-ttu-id="629ca-173">En hello **configuración de SAML** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="629ca-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![Qué es Azure AD Connect][14]

     <span data-ttu-id="629ca-175">a.</span><span class="sxs-lookup"><span data-stu-id="629ca-175">a.</span></span> <span data-ttu-id="629ca-176">En **Identificador único**, seleccione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="629ca-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="629ca-177">b.</span><span class="sxs-lookup"><span data-stu-id="629ca-177">b.</span></span> <span data-ttu-id="629ca-178">En **El identificador único se asigna a**, seleccione **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="629ca-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="629ca-179">c.</span><span class="sxs-lookup"><span data-stu-id="629ca-179">c.</span></span> <span data-ttu-id="629ca-180">tooupload el archivo de metadatos descargado, haga clic en **examinar** tooselect archivo de hello y, a continuación, **cargar archivo**.</span><span class="sxs-lookup"><span data-stu-id="629ca-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="629ca-181">d.</span><span class="sxs-lookup"><span data-stu-id="629ca-181">d.</span></span> <span data-ttu-id="629ca-182">configuración de hello tootest, haga clic en **Ejecutar prueba**.</span><span class="sxs-lookup"><span data-stu-id="629ca-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="629ca-183">Necesita toowait para mensajes de bienvenida "*prueba SAML de hello es completa. Cierre esta ventana* ".</span><span class="sxs-lookup"><span data-stu-id="629ca-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="629ca-184">A continuación, cierre la ventana del explorador abierto de Hola.</span><span class="sxs-lookup"><span data-stu-id="629ca-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="629ca-185">Hola **habilitar SAML** casilla de verificación solo está habilitada si se ha completado la prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="629ca-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="629ca-186">e.</span><span class="sxs-lookup"><span data-stu-id="629ca-186">e.</span></span> <span data-ttu-id="629ca-187">Seleccione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="629ca-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="629ca-188">f.</span><span class="sxs-lookup"><span data-stu-id="629ca-188">f.</span></span> <span data-ttu-id="629ca-189">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="629ca-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="629ca-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="629ca-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="629ca-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="629ca-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="629ca-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="629ca-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="629ca-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ca-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="629ca-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="629ca-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="629ca-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="629ca-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="629ca-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="629ca-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="629ca-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="629ca-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="629ca-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="629ca-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="629ca-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="629ca-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="629ca-205">a.</span><span class="sxs-lookup"><span data-stu-id="629ca-205">a.</span></span> <span data-ttu-id="629ca-206">Hola **nombre** cuadro de texto, nombre de tipo como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="629ca-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="629ca-207">b.</span><span class="sxs-lookup"><span data-stu-id="629ca-207">b.</span></span> <span data-ttu-id="629ca-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="629ca-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="629ca-209">c.</span><span class="sxs-lookup"><span data-stu-id="629ca-209">c.</span></span> <span data-ttu-id="629ca-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="629ca-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="629ca-211">d.</span><span class="sxs-lookup"><span data-stu-id="629ca-211">d.</span></span> <span data-ttu-id="629ca-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="629ca-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="629ca-213">Creación de un usuario de prueba de Halogen Software</span><span class="sxs-lookup"><span data-stu-id="629ca-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="629ca-214">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon halógeno software.</span><span class="sxs-lookup"><span data-stu-id="629ca-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="629ca-215">**toocreate un usuario llamado Britta Simon en Software halógenas, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="629ca-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="629ca-216">Inicio de sesión tooyour **Software halógenas** aplicación como administrador.</span><span class="sxs-lookup"><span data-stu-id="629ca-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="629ca-217">Haga clic en hello **usuario Center** ficha y, a continuación, haga clic en **Create User**.</span><span class="sxs-lookup"><span data-stu-id="629ca-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![Qué es Azure AD Connect][300]  

3. <span data-ttu-id="629ca-219">En hello **nuevo usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="629ca-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![Qué es Azure AD Connect][301]

    <span data-ttu-id="629ca-221">a.</span><span class="sxs-lookup"><span data-stu-id="629ca-221">a.</span></span> <span data-ttu-id="629ca-222">Hola **nombre** cuadro de texto Nombre de usuario de hello como tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="629ca-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="629ca-223">b.</span><span class="sxs-lookup"><span data-stu-id="629ca-223">b.</span></span> <span data-ttu-id="629ca-224">Hola **Last Name** cuadro de texto, escriba Apellidos del usuario de hello como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="629ca-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="629ca-225">c.</span><span class="sxs-lookup"><span data-stu-id="629ca-225">c.</span></span> <span data-ttu-id="629ca-226">Hola **nombre de usuario** cuadro de texto, tipo **Britta Simon**, nombre de usuario de hello en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="629ca-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="629ca-227">d.</span><span class="sxs-lookup"><span data-stu-id="629ca-227">d.</span></span> <span data-ttu-id="629ca-228">Hola **contraseña** cuadro de texto, escriba una contraseña para Bárbara.</span><span class="sxs-lookup"><span data-stu-id="629ca-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="629ca-229">e.</span><span class="sxs-lookup"><span data-stu-id="629ca-229">e.</span></span> <span data-ttu-id="629ca-230">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="629ca-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="629ca-231">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ca-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="629ca-232">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHalogen Software.</span><span class="sxs-lookup"><span data-stu-id="629ca-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="629ca-234">**tooassign Britta Simon tooHalogen Software, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="629ca-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="629ca-235">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="629ca-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="629ca-237">En la lista de aplicaciones de hello, seleccione **Software halógenas**.</span><span class="sxs-lookup"><span data-stu-id="629ca-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="629ca-239">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="629ca-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="629ca-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="629ca-241">Click **Add** button.</span></span> <span data-ttu-id="629ca-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="629ca-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="629ca-244">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="629ca-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="629ca-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="629ca-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="629ca-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="629ca-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="629ca-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="629ca-247">Testing single sign-on</span></span>

<span data-ttu-id="629ca-248">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="629ca-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="629ca-249">Al hacer clic en icono de Software halógeno Hola Hola Panel de acceso, deberá obtener la aplicación de Software halógenas tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="629ca-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="629ca-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="629ca-250">Additional resources</span></span>

* [<span data-ttu-id="629ca-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="629ca-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="629ca-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="629ca-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
