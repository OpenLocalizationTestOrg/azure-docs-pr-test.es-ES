---
title: "Tutorial: Integración de Azure Active Directory con 123ContactForm | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="96607-103">Tutorial: integración de Azure Active Directory con 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="96607-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="96607-104">En este tutorial, aprenderá cómo toointegrate 123ContactForm con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96607-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96607-105">Integración 123ContactForm con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="96607-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96607-106">Puede controlar en Azure AD que tenga acceso too123ContactForm</span><span class="sxs-lookup"><span data-stu-id="96607-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="96607-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión too123ContactForm (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96607-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96607-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="96607-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="96607-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96607-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96607-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96607-110">Prerequisites</span></span>

<span data-ttu-id="96607-111">integración de Azure AD con 123ContactForm tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="96607-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="96607-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96607-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96607-113">Una suscripción habilitada para el inicio de sesión único en 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="96607-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96607-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="96607-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96607-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="96607-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96607-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="96607-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96607-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96607-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96607-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="96607-118">Scenario description</span></span>
<span data-ttu-id="96607-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="96607-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96607-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="96607-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96607-121">Agregar 123ContactForm desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="96607-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="96607-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96607-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="96607-123">Agregar 123ContactForm desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="96607-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="96607-124">integración de hello tooconfigure de 123ContactForm en Azure AD, deberá tooadd 123ContactForm de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="96607-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96607-125">**tooadd 123ContactForm de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="96607-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96607-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="96607-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96607-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="96607-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96607-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="96607-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="96607-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="96607-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="96607-133">En el cuadro de búsqueda de hello, escriba **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="96607-133">In hello search box, type **123ContactForm**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="96607-135">En el panel de resultados de hello, seleccione **123ContactForm**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="96607-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96607-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96607-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96607-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 123ContactForm con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="96607-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="96607-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en 123ContactForm es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96607-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="96607-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en 123ContactForm debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="96607-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="96607-141">En 123ContactForm, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="96607-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96607-142">tooconfigure y prueba de inicio de sesión único en Azure AD con 123ContactForm, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="96607-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96607-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="96607-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96607-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96607-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96607-145">**[Crear un usuario de prueba 123ContactForm](#creating-a-123contactform-test-user)**  -toohave un equivalente de Britta Simon en 123ContactForm que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="96607-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96607-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="96607-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96607-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="96607-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96607-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96607-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96607-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="96607-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="96607-150">**inicio de sesión único en Azure AD tooconfigure con 123ContactForm, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="96607-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="96607-151">En el portal de Azure, en Hola Hola **123ContactForm** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="96607-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="96607-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="96607-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="96607-155">En hello **123ContactForm dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="96607-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="96607-157">a.</span><span class="sxs-lookup"><span data-stu-id="96607-157">a.</span></span> <span data-ttu-id="96607-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="96607-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="96607-159">b.</span><span class="sxs-lookup"><span data-stu-id="96607-159">b.</span></span> <span data-ttu-id="96607-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="96607-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="96607-161">Si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="96607-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="96607-163">a.</span><span class="sxs-lookup"><span data-stu-id="96607-163">a.</span></span> <span data-ttu-id="96607-164">Haga clic en hello **mostrar avanzadas de configuración de direcciones URL** opción</span><span class="sxs-lookup"><span data-stu-id="96607-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="96607-165">b.</span><span class="sxs-lookup"><span data-stu-id="96607-165">b.</span></span> <span data-ttu-id="96607-166">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="96607-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96607-167">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="96607-167">These values are not real.</span></span> <span data-ttu-id="96607-168">Necesitará tooupdate comprendido entre estos real direcciones URL y el identificador que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="96607-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="96607-169">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="96607-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="96607-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="96607-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="96607-173">tooconfigure inicio de sesión único en **123ContactForm** en paralelo, vaya demasiado[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="96607-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="96607-175">a.</span><span class="sxs-lookup"><span data-stu-id="96607-175">a.</span></span> <span data-ttu-id="96607-176">Hola **correo electrónico** cuadro de texto, correo electrónico de Hola de tipo de hello usuario sólo</span><span class="sxs-lookup"><span data-stu-id="96607-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="96607-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="96607-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="96607-178">b.</span><span class="sxs-lookup"><span data-stu-id="96607-178">b.</span></span> <span data-ttu-id="96607-179">Haga clic en **cargar** y examinar Hola archivo Metadata XML, que ha descargado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="96607-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="96607-180">c.</span><span class="sxs-lookup"><span data-stu-id="96607-180">c.</span></span> <span data-ttu-id="96607-181">Haga clic en **ENVIAR FORMULARIO**.</span><span class="sxs-lookup"><span data-stu-id="96607-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="96607-182">En hello **Microsoft Azure AD - inicio de sesión único - configurar opciones de aplicación** realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="96607-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="96607-184">a.</span><span class="sxs-lookup"><span data-stu-id="96607-184">a.</span></span> <span data-ttu-id="96607-185">Si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**, Hola copia **identificador** valor para la instancia y péguelo en **identificador** cuadro de texto en **123ContactForm dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="96607-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="96607-186">b.</span><span class="sxs-lookup"><span data-stu-id="96607-186">b.</span></span> <span data-ttu-id="96607-187">Si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**, Hola copia **dirección URL de respuesta** valor para la instancia y péguelo en **dirección URL de respuesta** cuadro de texto en **123ContactForm dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="96607-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="96607-188">c.</span><span class="sxs-lookup"><span data-stu-id="96607-188">c.</span></span> <span data-ttu-id="96607-189">Si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, Hola copia **URL de inicio de sesión** valor para la instancia y péguelo en **dirección URL de inicio de sesión** cuadro de texto en **123ContactForm dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="96607-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="96607-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="96607-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96607-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="96607-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96607-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96607-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96607-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="96607-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="96607-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="96607-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="96607-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="96607-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96607-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="96607-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96607-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="96607-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96607-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="96607-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96607-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="96607-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96607-205">a.</span><span class="sxs-lookup"><span data-stu-id="96607-205">a.</span></span> <span data-ttu-id="96607-206">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96607-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96607-207">b.</span><span class="sxs-lookup"><span data-stu-id="96607-207">b.</span></span> <span data-ttu-id="96607-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96607-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96607-209">c.</span><span class="sxs-lookup"><span data-stu-id="96607-209">c.</span></span> <span data-ttu-id="96607-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="96607-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="96607-211">d.</span><span class="sxs-lookup"><span data-stu-id="96607-211">d.</span></span> <span data-ttu-id="96607-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="96607-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="96607-213">Crear un usuario de prueba de 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="96607-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="96607-214">Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de que los usuarios de autenticación se creará en la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="96607-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96607-215">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="96607-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96607-216">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso too123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="96607-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="96607-218">**tooassign Britta Simon too123ContactForm, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="96607-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="96607-219">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="96607-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="96607-221">En la lista de aplicaciones de hello, seleccione **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="96607-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="96607-223">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="96607-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="96607-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="96607-225">Click **Add** button.</span></span> <span data-ttu-id="96607-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="96607-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="96607-228">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="96607-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96607-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="96607-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96607-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="96607-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96607-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="96607-231">Testing single sign-on</span></span>

<span data-ttu-id="96607-232">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="96607-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96607-233">Al hacer clic en icono de 123ContactForm Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour 123ContactForm aplicación.</span><span class="sxs-lookup"><span data-stu-id="96607-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="96607-234">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="96607-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96607-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="96607-235">Additional resources</span></span>

* [<span data-ttu-id="96607-236">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96607-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96607-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96607-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

