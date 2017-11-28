---
title: "Tutorial: Integración de Azure Active Directory con 10,000ft Plans | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y 10.000 pies planes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="14c9e-103">Tutorial: integración de Azure Active Directory con 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="14c9e-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="14c9e-104">En este tutorial, aprenderá cómo toointegrate 10.000 pies planes con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14c9e-104">In this tutorial, you learn how toointegrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14c9e-105">Integrar planes de 10.000 pies con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="14c9e-105">Integrating 10,000ft Plans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="14c9e-106">Puede controlar en Azure AD que tenga acceso too10, 000ft planes</span><span class="sxs-lookup"><span data-stu-id="14c9e-106">You can control in Azure AD who has access too10,000ft Plans</span></span>
- <span data-ttu-id="14c9e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión too10, planes de 000ft (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14c9e-107">You can enable your users tooautomatically get signed-on too10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14c9e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="14c9e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="14c9e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14c9e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14c9e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="14c9e-110">Prerequisites</span></span>

<span data-ttu-id="14c9e-111">integración de Azure AD con planes de 10.000 pies tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="14c9e-111">tooconfigure Azure AD integration with 10,000ft Plans, you need hello following items:</span></span>

- <span data-ttu-id="14c9e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14c9e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14c9e-113">Una suscripción habilitada para el inicio de sesión único en 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="14c9e-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14c9e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="14c9e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14c9e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="14c9e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14c9e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="14c9e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14c9e-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14c9e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14c9e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="14c9e-118">Scenario description</span></span>
<span data-ttu-id="14c9e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="14c9e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14c9e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="14c9e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14c9e-121">Agregar 10.000 pies planes de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="14c9e-121">Adding 10,000ft Plans from hello gallery</span></span>
2. <span data-ttu-id="14c9e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14c9e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-hello-gallery"></a><span data-ttu-id="14c9e-123">Agregar 10.000 pies planes de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="14c9e-123">Adding 10,000ft Plans from hello gallery</span></span>
<span data-ttu-id="14c9e-124">integración de hello tooconfigure de planes de 10.000 pies en Azure AD, necesita tooadd 10.000 pies planes de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="14c9e-124">tooconfigure hello integration of 10,000ft Plans into Azure AD, you need tooadd 10,000ft Plans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="14c9e-125">**Planes de tooadd 10.000 pies de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14c9e-125">**tooadd 10,000ft Plans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="14c9e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="14c9e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="14c9e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="14c9e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="14c9e-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="14c9e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="14c9e-133">En el cuadro de búsqueda de hello, escriba **planes de 10.000 pies**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-133">In hello search box, type **10,000ft Plans**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="14c9e-135">En el panel de resultados de hello, seleccione **planes de 10.000 pies**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="14c9e-135">In hello results panel, select **10,000ft Plans**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="14c9e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14c9e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="14c9e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 10,000ft Plans con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="14c9e-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="14c9e-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en los planes de 10.000 pies es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14c9e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 10,000ft Plans is tooa user in Azure AD.</span></span> <span data-ttu-id="14c9e-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en 10.000 pies planes debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="14c9e-140">In other words, a link relationship between an Azure AD user and hello related user in 10,000ft Plans needs toobe established.</span></span>

<span data-ttu-id="14c9e-141">En los planes de 10.000 pies, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="14c9e-141">In 10,000ft Plans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="14c9e-142">tooconfigure y prueba de inicio de sesión único en Azure AD con planes de 10.000 pies, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="14c9e-142">tooconfigure and test Azure AD single sign-on with 10,000ft Plans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="14c9e-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="14c9e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="14c9e-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14c9e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14c9e-145">**[Crear un 10.000 pies planes de usuario de prueba](#creating-a-10000ft-plans-test-user)**  -toohave un equivalente de Britta Simon en 10.000 pies decir planes vinculados representación toohello Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="14c9e-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - toohave a counterpart of Britta Simon in 10,000ft Plans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="14c9e-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="14c9e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14c9e-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="14c9e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="14c9e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14c9e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="14c9e-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de planes de 10.000 pies.</span><span class="sxs-lookup"><span data-stu-id="14c9e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="14c9e-150">**inicio de sesión único en tooconfigure Azure AD con planes de 10.000 pies, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14c9e-150">**tooconfigure Azure AD single sign-on with 10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="14c9e-151">En el portal de Azure, en Hola Hola **planes de 10.000 pies** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-151">In hello Azure portal, on hello **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="14c9e-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="14c9e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="14c9e-155">En hello **10.000 ft planes de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="14c9e-155">On hello **10,000ft Plans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="14c9e-157">a.</span><span class="sxs-lookup"><span data-stu-id="14c9e-157">a.</span></span> <span data-ttu-id="14c9e-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="14c9e-158">In hello **Sign-on URL** textbox, type hello URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="14c9e-159">b.</span><span class="sxs-lookup"><span data-stu-id="14c9e-159">b.</span></span> <span data-ttu-id="14c9e-160">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="14c9e-160">In hello **Identifier** textbox, type hello URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14c9e-161">Hola valor para **identificador** es distinto si tiene un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="14c9e-161">hello value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="14c9e-162">Póngase en contacto con [equipo de soporte técnico de planes de 10.000 pies](https://www.10000ft.com/plans/support) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="14c9e-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="14c9e-163">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="14c9e-163">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="14c9e-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="14c9e-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="14c9e-167">En hello **10.000 pies planes configuración** sección, haga clic en **configurar los planes de 10.000 pies** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="14c9e-167">On hello **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="14c9e-168">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="14c9e-168">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="14c9e-170">tooconfigure inicio de sesión único en **planes de 10.000 pies** lado, necesita hello toosend descargado **Certificate(Raw), dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado[ equipo de soporte técnico de planes de 10.000 pies](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="14c9e-170">tooconfigure single sign-on on **10,000ft Plans** side, you need toosend hello downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="14c9e-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="14c9e-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="14c9e-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="14c9e-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="14c9e-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14c9e-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="14c9e-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14c9e-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="14c9e-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="14c9e-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="14c9e-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14c9e-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="14c9e-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="14c9e-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14c9e-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14c9e-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="14c9e-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14c9e-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="14c9e-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14c9e-186">a.</span><span class="sxs-lookup"><span data-stu-id="14c9e-186">a.</span></span> <span data-ttu-id="14c9e-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14c9e-188">b.</span><span class="sxs-lookup"><span data-stu-id="14c9e-188">b.</span></span> <span data-ttu-id="14c9e-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="14c9e-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14c9e-190">c.</span><span class="sxs-lookup"><span data-stu-id="14c9e-190">c.</span></span> <span data-ttu-id="14c9e-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="14c9e-192">d.</span><span class="sxs-lookup"><span data-stu-id="14c9e-192">d.</span></span> <span data-ttu-id="14c9e-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="14c9e-194">Creación de un usuario de prueba de 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="14c9e-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="14c9e-195">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en los planes de 10.000 pies.</span><span class="sxs-lookup"><span data-stu-id="14c9e-195">hello objective of this section is toocreate a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="14c9e-196">10,000ft Plans admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="14c9e-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="14c9e-197">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="14c9e-197">There is no action item for you in this section.</span></span> <span data-ttu-id="14c9e-198">Si no existe todavía, se crea un usuario nuevo durante un tooaccess de intento de 10.000 pies planes.</span><span class="sxs-lookup"><span data-stu-id="14c9e-198">A new user is created during an attempt tooaccess 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="14c9e-199">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de planes de 10.000 pies](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="14c9e-199">If you need toocreate a user manually, you need toocontact hello [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="14c9e-200">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="14c9e-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="14c9e-201">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso too10, planes de 000ft.</span><span class="sxs-lookup"><span data-stu-id="14c9e-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too10,000ft Plans.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="14c9e-203">**tooassign Britta Simon too10, planes de 000ft, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14c9e-203">**tooassign Britta Simon too10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="14c9e-204">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="14c9e-206">En la lista de aplicaciones de hello, seleccione **planes de 10.000 pies**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-206">In hello applications list, select **10,000ft Plans**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="14c9e-208">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="14c9e-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-210">Click **Add** button.</span></span> <span data-ttu-id="14c9e-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="14c9e-213">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="14c9e-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="14c9e-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14c9e-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="14c9e-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="14c9e-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="14c9e-216">Testing single sign-on</span></span>

<span data-ttu-id="14c9e-217">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="14c9e-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="14c9e-218">Al hacer clic en hello 10.000 pies planes de icono en el Panel de acceso de hello, deberá obtener la aplicación de planes de 10.000 pies tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="14c9e-218">When you click hello 10,000ft Plans tile in hello Access Panel, you should get automatically signed-on tooyour 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="14c9e-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="14c9e-219">Additional resources</span></span>

* [<span data-ttu-id="14c9e-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14c9e-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14c9e-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14c9e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

