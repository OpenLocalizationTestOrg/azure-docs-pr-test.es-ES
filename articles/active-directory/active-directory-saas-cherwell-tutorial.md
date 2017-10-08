---
title: "Tutorial: Integración de Azure Active Directory con Cherwell | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Cherwell."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: jeedes
ms.openlocfilehash: a67b3d346a6f7b43a7e87fb4d9c533f9363f2e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="05c2e-103">Tutorial: Integración de Azure Active Directory con Cherwell</span><span class="sxs-lookup"><span data-stu-id="05c2e-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>

<span data-ttu-id="05c2e-104">En este tutorial, aprenderá cómo toointegrate Cherwell con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05c2e-104">In this tutorial, you learn how toointegrate Cherwell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05c2e-105">Integración de Cherwell con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="05c2e-105">Integrating Cherwell with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05c2e-106">Puede controlar en Azure AD que tenga acceso tooCherwell</span><span class="sxs-lookup"><span data-stu-id="05c2e-106">You can control in Azure AD who has access tooCherwell</span></span>
- <span data-ttu-id="05c2e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCherwell (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c2e-107">You can enable your users tooautomatically get signed-on tooCherwell (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05c2e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="05c2e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="05c2e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05c2e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05c2e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="05c2e-110">Prerequisites</span></span>

<span data-ttu-id="05c2e-111">integración de Azure AD con Cherwell tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="05c2e-111">tooconfigure Azure AD integration with Cherwell, you need hello following items:</span></span>

- <span data-ttu-id="05c2e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05c2e-113">Una suscripción habilitada para inicio de sesión único en Cherwell</span><span class="sxs-lookup"><span data-stu-id="05c2e-113">A Cherwell single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05c2e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="05c2e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05c2e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="05c2e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05c2e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05c2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05c2e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05c2e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05c2e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="05c2e-118">Scenario description</span></span>
<span data-ttu-id="05c2e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="05c2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05c2e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="05c2e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05c2e-121">Agregar Cherwell desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="05c2e-121">Adding Cherwell from hello gallery</span></span>
2. <span data-ttu-id="05c2e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cherwell-from-hello-gallery"></a><span data-ttu-id="05c2e-123">Agregar Cherwell desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="05c2e-123">Adding Cherwell from hello gallery</span></span>
<span data-ttu-id="05c2e-124">integración de hello tooconfigure de Cherwell en Azure AD, deberá tooadd Cherwell de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="05c2e-124">tooconfigure hello integration of Cherwell into Azure AD, you need tooadd Cherwell from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="05c2e-125">**tooadd Cherwell de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="05c2e-125">**tooadd Cherwell from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="05c2e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="05c2e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05c2e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="05c2e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="05c2e-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05c2e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="05c2e-133">En el cuadro de búsqueda de hello, escriba **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-133">In hello search box, type **Cherwell**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_search.png)

5. <span data-ttu-id="05c2e-135">En el panel de resultados de hello, seleccione **Cherwell**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="05c2e-135">In hello results panel, select **Cherwell**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05c2e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c2e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05c2e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Cherwell con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="05c2e-138">In this section, you configure and test Azure AD single sign-on with Cherwell based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05c2e-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Cherwell es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05c2e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cherwell is tooa user in Azure AD.</span></span> <span data-ttu-id="05c2e-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Cherwell debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="05c2e-140">In other words, a link relationship between an Azure AD user and hello related user in Cherwell needs toobe established.</span></span>

<span data-ttu-id="05c2e-141">En Cherwell, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c2e-141">In Cherwell, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="05c2e-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Cherwell, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="05c2e-142">tooconfigure and test Azure AD single sign-on with Cherwell, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05c2e-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="05c2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05c2e-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05c2e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05c2e-145">**[Crear un usuario de prueba de Cherwell](#creating-a-cherwell-test-user)**  -toohave un equivalente de Britta Simon en Cherwell que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="05c2e-145">**[Creating a Cherwell test user](#creating-a-cherwell-test-user)** - toohave a counterpart of Britta Simon in Cherwell that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05c2e-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="05c2e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05c2e-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="05c2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05c2e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c2e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05c2e-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Cherwell.</span><span class="sxs-lookup"><span data-stu-id="05c2e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cherwell application.</span></span>

<span data-ttu-id="05c2e-150">**inicio de sesión único en Azure AD tooconfigure con Cherwell, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="05c2e-150">**tooconfigure Azure AD single sign-on with Cherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="05c2e-151">En el portal de Azure, en Hola Hola **Cherwell** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-151">In hello Azure portal, on hello **Cherwell** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="05c2e-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="05c2e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_samlbase.png)

3. <span data-ttu-id="05c2e-155">En hello **Cherwell dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="05c2e-155">On hello **Cherwell Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_url.png)

    <span data-ttu-id="05c2e-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.cherwellondemand.com/cherwellclient`</span><span class="sxs-lookup"><span data-stu-id="05c2e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.cherwellondemand.com/cherwellclient`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05c2e-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="05c2e-158">This value is not real.</span></span> <span data-ttu-id="05c2e-159">Actualizar este valor con la URL de inicio de sesión real de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c2e-159">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="05c2e-160">Póngase en contacto con [equipo de soporte técnico de Cherwell](https://csm.cherwell.com/contact) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="05c2e-160">Contact [Cherwell support team](https://csm.cherwell.com/contact) tooget this value.</span></span>
 
4. <span data-ttu-id="05c2e-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="05c2e-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_certificate.png) 

5. <span data-ttu-id="05c2e-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="05c2e-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cherwell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05c2e-165">En hello **configuración de Cherwell** sección, haga clic en **configurar Cherwell** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="05c2e-165">On hello **Cherwell Configuration** section, click **Configure Cherwell** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="05c2e-166">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="05c2e-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_configure.png) 

7. <span data-ttu-id="05c2e-168">tooconfigure inicio de sesión único en **Cherwell** lado, necesita hello toosend descargado **certificado (Base64)**, **SAML Single Sign-On dirección URL del servicio**, y  **Id. de entidad SAML** demasiado[equipo de soporte técnico de Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="05c2e-168">tooconfigure single sign-on on **Cherwell** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Cherwell support team](https://csm.cherwell.com/contact).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="05c2e-169">El equipo de soporte técnico de Cherwell tiene la configuración real del SSO toodo Hola.</span><span class="sxs-lookup"><span data-stu-id="05c2e-169">Your Cherwell support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="05c2e-170">Cuando SSO se haya habilitado en su suscripción recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="05c2e-170">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    
> [!TIP]
> <span data-ttu-id="05c2e-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="05c2e-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05c2e-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="05c2e-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05c2e-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05c2e-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05c2e-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c2e-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="05c2e-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="05c2e-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="05c2e-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="05c2e-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05c2e-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="05c2e-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05c2e-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05c2e-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c2e-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05c2e-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="05c2e-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05c2e-186">a.</span><span class="sxs-lookup"><span data-stu-id="05c2e-186">a.</span></span> <span data-ttu-id="05c2e-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05c2e-188">b.</span><span class="sxs-lookup"><span data-stu-id="05c2e-188">b.</span></span> <span data-ttu-id="05c2e-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05c2e-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05c2e-190">c.</span><span class="sxs-lookup"><span data-stu-id="05c2e-190">c.</span></span> <span data-ttu-id="05c2e-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="05c2e-192">d.</span><span class="sxs-lookup"><span data-stu-id="05c2e-192">d.</span></span> <span data-ttu-id="05c2e-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-193">Click **Create**.</span></span>
 
### <a name="creating-a-cherwell-test-user"></a><span data-ttu-id="05c2e-194">Creación de un usuario de prueba de Cherwell</span><span class="sxs-lookup"><span data-stu-id="05c2e-194">Creating a Cherwell test user</span></span>

<span data-ttu-id="05c2e-195">toolog de los usuarios de Azure AD tooenable en tooCherwell, se les deben aprovisionar en Cherwell.</span><span class="sxs-lookup"><span data-stu-id="05c2e-195">tooenable Azure AD users toolog in tooCherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="05c2e-196">En caso de hello de Cherwell, cuentas de usuario de hello debe toobe creado por la [equipo de soporte técnico de Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="05c2e-196">In hello case of Cherwell, hello user accounts need toobe created by your [Cherwell support team](https://csm.cherwell.com/contact).</span></span>

>[!NOTE]
><span data-ttu-id="05c2e-197">Puede usar cualquier otra Cherwell usuario cuenta herramienta de creación o las API proporcionadas por Cherwell tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="05c2e-197">You can use any other Cherwell user account creation tools or APIs provided by Cherwell tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="05c2e-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c2e-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="05c2e-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCherwell.</span><span class="sxs-lookup"><span data-stu-id="05c2e-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCherwell.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="05c2e-201">**tooassign Britta Simon tooCherwell, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="05c2e-201">**tooassign Britta Simon tooCherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="05c2e-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="05c2e-204">En la lista de aplicaciones de hello, seleccione **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-204">In hello applications list, select **Cherwell**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_app.png) 

3. <span data-ttu-id="05c2e-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="05c2e-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-208">Click **Add** button.</span></span> <span data-ttu-id="05c2e-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="05c2e-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c2e-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05c2e-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05c2e-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="05c2e-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05c2e-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="05c2e-214">Testing single sign-on</span></span>

<span data-ttu-id="05c2e-215">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="05c2e-215">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="05c2e-216">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05c2e-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05c2e-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="05c2e-217">Additional resources</span></span>

* [<span data-ttu-id="05c2e-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05c2e-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05c2e-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05c2e-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_203.png

