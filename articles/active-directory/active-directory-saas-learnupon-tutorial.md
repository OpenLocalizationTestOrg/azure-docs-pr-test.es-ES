---
title: "Tutorial: Integración de Azure Active Directory con LearnUpon | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="4a859-103">Tutorial: Integración de Azure Active Directory con LearnUpon</span><span class="sxs-lookup"><span data-stu-id="4a859-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="4a859-104">En este tutorial, aprenderá cómo toointegrate LearnUpon con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a859-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a859-105">Integración LearnUpon con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4a859-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a859-106">Puede controlar en Azure AD que tenga acceso tooLearnUpon</span><span class="sxs-lookup"><span data-stu-id="4a859-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="4a859-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLearnUpon (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a859-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a859-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4a859-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4a859-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a859-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a859-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4a859-110">Prerequisites</span></span>

<span data-ttu-id="4a859-111">integración de Azure AD con LearnUpon tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4a859-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="4a859-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a859-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a859-113">Una suscripción habilitada para el inicio de sesión único en LearnUpon</span><span class="sxs-lookup"><span data-stu-id="4a859-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a859-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4a859-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a859-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4a859-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a859-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4a859-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a859-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a859-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a859-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4a859-118">Scenario description</span></span>
<span data-ttu-id="4a859-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4a859-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a859-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4a859-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a859-121">Agregar LearnUpon desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4a859-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="4a859-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a859-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="4a859-123">Agregar LearnUpon desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4a859-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="4a859-124">integración de hello tooconfigure de LearnUpon en Azure AD, deberá tooadd LearnUpon de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4a859-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a859-125">**tooadd LearnUpon de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a859-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a859-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4a859-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4a859-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4a859-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a859-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a859-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4a859-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a859-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4a859-133">En el cuadro de búsqueda de hello, escriba **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="4a859-133">In hello search box, type **LearnUpon**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="4a859-135">En el panel de resultados de hello, seleccione **LearnUpon**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4a859-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a859-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a859-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a859-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LearnUpon con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4a859-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a859-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LearnUpon es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a859-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="4a859-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LearnUpon debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4a859-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="4a859-141">En LearnUpon, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a859-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4a859-142">tooconfigure y prueba de inicio de sesión único en Azure AD con LearnUpon, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4a859-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a859-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4a859-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a859-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a859-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a859-145">**[Crear un usuario de prueba LearnUpon](#creating-a-learnupon-test-user)**  -toohave un equivalente de Britta Simon en LearnUpon que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4a859-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a859-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4a859-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a859-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4a859-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a859-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a859-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a859-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="4a859-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="4a859-150">**inicio de sesión único en Azure AD tooconfigure con LearnUpon, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a859-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a859-151">En el portal de Azure, en Hola Hola **LearnUpon** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4a859-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4a859-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4a859-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="4a859-155">En hello **LearnUpon dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4a859-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="4a859-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="4a859-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a859-158">Tenga en cuenta que esto no es un valor real Hola.</span><span class="sxs-lookup"><span data-stu-id="4a859-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="4a859-159">tiene este valor con la dirección URL de respuesta real hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="4a859-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="4a859-160">tooget este valor póngase en contacto con [equipo de soporte técnico de LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="4a859-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="4a859-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4a859-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="4a859-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4a859-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a859-165">En hello **LearnUpon configuración** sección, haga clic en **configurar LearnUpon** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4a859-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4a859-166">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="4a859-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="4a859-168">Abra otra instancia del explorador e inicie sesión en LearnUpon con una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="4a859-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="4a859-169">Haga clic en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="4a859-169">Click hello **settings** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="4a859-171">Haga clic en **Single Sign On - SAML**y, a continuación, haga clic en **configuración General** tooconfigure configuración de SAML.</span><span class="sxs-lookup"><span data-stu-id="4a859-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="4a859-173">Hola **configuración General** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4a859-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="4a859-175">a.</span><span class="sxs-lookup"><span data-stu-id="4a859-175">a.</span></span> <span data-ttu-id="4a859-176">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="4a859-176">Select **Enabled**.</span></span>

    <span data-ttu-id="4a859-177">b.</span><span class="sxs-lookup"><span data-stu-id="4a859-177">b.</span></span> <span data-ttu-id="4a859-178">Seleccione la **versión** **2.0**.</span><span class="sxs-lookup"><span data-stu-id="4a859-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="4a859-179">c.</span><span class="sxs-lookup"><span data-stu-id="4a859-179">c.</span></span> <span data-ttu-id="4a859-180">En **Skip conditions** (Omitir condiciones), haga clic en **No**.</span><span class="sxs-lookup"><span data-stu-id="4a859-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="4a859-181">d.</span><span class="sxs-lookup"><span data-stu-id="4a859-181">d.</span></span> <span data-ttu-id="4a859-182">Hola **publicar Token de SAML param nombre** cuadro de texto Nombre de solicitud post parámetro toohello dirección URL del consumidor SAML indicada anteriormente que contiene toobe de aserción de SAML de hello comprueban y autentican - por ejemplo hello de tipo  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="4a859-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="4a859-183">e.</span><span class="sxs-lookup"><span data-stu-id="4a859-183">e.</span></span> <span data-ttu-id="4a859-184">Hola **formato de nombre de identificador** cuadro de texto, valor de Hola de tipo que indica dónde en los usuarios de Hola de aserción de SAML identificador (dirección de correo electrónico) reside - por ejemplo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="4a859-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="4a859-185">f.</span><span class="sxs-lookup"><span data-stu-id="4a859-185">f.</span></span> <span data-ttu-id="4a859-186">Hola **identificar la ubicación del proveedor** cuadro de texto, valor de Hola de tipo que indica dónde hello se envían tooif a los usuarios hagan clic en el icono cargada desde la pantalla de inicio de sesión de portal Azure.</span><span class="sxs-lookup"><span data-stu-id="4a859-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="4a859-187">g.</span><span class="sxs-lookup"><span data-stu-id="4a859-187">g.</span></span> <span data-ttu-id="4a859-188">Hola **cerrar sesión URL** cuadro de texto, pegue hello **dirección URL de cierre de sesión** que haya copiado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a859-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="4a859-189">h.</span><span class="sxs-lookup"><span data-stu-id="4a859-189">h.</span></span> <span data-ttu-id="4a859-190">Haga clic en **administrar huellas dactilares**y, a continuación, cargar la huella dactilar de Hola del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="4a859-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="4a859-191">Haga clic en **configuración de usuario**y, a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4a859-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="4a859-193">a.</span><span class="sxs-lookup"><span data-stu-id="4a859-193">a.</span></span> <span data-ttu-id="4a859-194">Hola **formato del identificador de nombre** cuadro de texto, valor de tipo de Hola que nos indica cuando, en su firstname de los usuarios de aserción de SAML Hola reside - por ejemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="4a859-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="4a859-195">b.</span><span class="sxs-lookup"><span data-stu-id="4a859-195">b.</span></span> <span data-ttu-id="4a859-196">Hola **formato de identificador de nombre de último** cuadro de texto, valor de tipo de Hola que nos indica cuando, en su lastname de los usuarios de aserción de SAML Hola reside - por ejemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="4a859-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="4a859-197">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4a859-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4a859-198">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4a859-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4a859-199">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a859-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a859-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a859-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a859-201">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4a859-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4a859-203">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a859-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a859-204">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4a859-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a859-206">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4a859-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a859-208">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a859-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a859-210">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4a859-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a859-212">a.</span><span class="sxs-lookup"><span data-stu-id="4a859-212">a.</span></span> <span data-ttu-id="4a859-213">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a859-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a859-214">b.</span><span class="sxs-lookup"><span data-stu-id="4a859-214">b.</span></span> <span data-ttu-id="4a859-215">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a859-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a859-216">c.</span><span class="sxs-lookup"><span data-stu-id="4a859-216">c.</span></span> <span data-ttu-id="4a859-217">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4a859-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a859-218">d.</span><span class="sxs-lookup"><span data-stu-id="4a859-218">d.</span></span> <span data-ttu-id="4a859-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4a859-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="4a859-220">Creación de un usuario de prueba de LearnUpon</span><span class="sxs-lookup"><span data-stu-id="4a859-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="4a859-221">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en LearnUpon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4a859-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="4a859-222">LearnUpon admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4a859-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4a859-223">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="4a859-223">There is no action item for you in this section.</span></span> <span data-ttu-id="4a859-224">Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="4a859-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="4a859-225">[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4a859-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="4a859-226">Si necesita un usuario toocreate manualmente, necesita toocontact [equipo de soporte técnico de LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="4a859-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4a859-227">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a859-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4a859-228">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLearnUpon.</span><span class="sxs-lookup"><span data-stu-id="4a859-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4a859-230">**tooassign Britta Simon tooLearnUpon, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a859-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a859-231">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a859-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4a859-233">En la lista de aplicaciones de hello, seleccione **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="4a859-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="4a859-235">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a859-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4a859-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4a859-237">Click **Add** button.</span></span> <span data-ttu-id="4a859-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4a859-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4a859-240">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a859-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a859-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a859-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a859-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4a859-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a859-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4a859-243">Testing single sign-on</span></span>

<span data-ttu-id="4a859-244">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4a859-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4a859-245">Al hacer clic en icono de LearnUpon Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour LearnUpon aplicación.</span><span class="sxs-lookup"><span data-stu-id="4a859-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="4a859-246">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a859-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a859-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4a859-247">Additional resources</span></span>

* [<span data-ttu-id="4a859-248">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a859-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a859-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a859-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

