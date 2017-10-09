---
title: "Tutorial: Integración de Azure Active Directory con Mixpanel | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 8da8aaefee3558c37babe3e10aeba4224ceffa16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="9cf75-103">Tutorial: Integración de Azure Active Directory con Mixpanel</span><span class="sxs-lookup"><span data-stu-id="9cf75-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="9cf75-104">En este tutorial, aprenderá cómo toointegrate Mixpanel con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cf75-104">In this tutorial, you learn how toointegrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cf75-105">Integración Mixpanel con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9cf75-105">Integrating Mixpanel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cf75-106">Puede controlar en Azure AD que tenga acceso tooMixpanel</span><span class="sxs-lookup"><span data-stu-id="9cf75-106">You can control in Azure AD who has access tooMixpanel</span></span>
- <span data-ttu-id="9cf75-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMixpanel (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf75-107">You can enable your users tooautomatically get signed-on tooMixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cf75-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9cf75-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9cf75-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cf75-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cf75-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9cf75-110">Prerequisites</span></span>

<span data-ttu-id="9cf75-111">integración de Azure AD con Mixpanel tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9cf75-111">tooconfigure Azure AD integration with Mixpanel, you need hello following items:</span></span>

- <span data-ttu-id="9cf75-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf75-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cf75-113">Una suscripción habilitada para inicio de sesión único en Mixpanel</span><span class="sxs-lookup"><span data-stu-id="9cf75-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cf75-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9cf75-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cf75-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9cf75-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cf75-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9cf75-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cf75-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cf75-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cf75-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9cf75-118">Scenario description</span></span>
<span data-ttu-id="9cf75-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9cf75-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cf75-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9cf75-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cf75-121">Agregar Mixpanel desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9cf75-121">Adding Mixpanel from hello gallery</span></span>
2. <span data-ttu-id="9cf75-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf75-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-hello-gallery"></a><span data-ttu-id="9cf75-123">Agregar Mixpanel desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9cf75-123">Adding Mixpanel from hello gallery</span></span>
<span data-ttu-id="9cf75-124">integración de hello tooconfigure de Mixpanel en Azure AD, deberá tooadd Mixpanel de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9cf75-124">tooconfigure hello integration of Mixpanel into Azure AD, you need tooadd Mixpanel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cf75-125">**tooadd Mixpanel de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf75-125">**tooadd Mixpanel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf75-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9cf75-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cf75-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cf75-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9cf75-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf75-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9cf75-133">En el cuadro de búsqueda de hello, escriba **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-133">In hello search box, type **Mixpanel**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="9cf75-135">En el panel de resultados de hello, seleccione **Mixpanel**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cf75-135">In hello results panel, select **Mixpanel**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cf75-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf75-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cf75-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mixpanel con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9cf75-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9cf75-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Mixpanel es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cf75-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mixpanel is tooa user in Azure AD.</span></span> <span data-ttu-id="9cf75-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Mixpanel debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9cf75-140">In other words, a link relationship between an Azure AD user and hello related user in Mixpanel needs toobe established.</span></span>

<span data-ttu-id="9cf75-141">En Mixpanel, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf75-141">In Mixpanel, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9cf75-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Mixpanel, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9cf75-142">tooconfigure and test Azure AD single sign-on with Mixpanel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cf75-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9cf75-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cf75-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cf75-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cf75-145">**[Crear un usuario de prueba Mixpanel](#creating-a-mixpanel-test-user)**  -toohave un equivalente de Britta Simon en Mixpanel que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9cf75-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - toohave a counterpart of Britta Simon in Mixpanel that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cf75-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9cf75-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cf75-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9cf75-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cf75-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf75-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cf75-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="9cf75-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="9cf75-150">**inicio de sesión único en Azure AD tooconfigure con Mixpanel, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf75-150">**tooconfigure Azure AD single sign-on with Mixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf75-151">En el portal de Azure, en Hola Hola **Mixpanel** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-151">In hello Azure portal, on hello **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9cf75-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9cf75-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="9cf75-155">En hello **Mixpanel dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9cf75-155">On hello **Mixpanel Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="9cf75-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="9cf75-157">In hello **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cf75-158">Regístrese en [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset seguridad de las credenciales de inicio de sesión y póngase en contacto con hello [equipo de soporte técnico de Mixpanel](mailto:support@mixpanel.com) tooenable configuración de SSO para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="9cf75-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset up your login credentials and  contact hello [Mixpanel support team](mailto:support@mixpanel.com) tooenable SSO settings for your tenant.</span></span> <span data-ttu-id="9cf75-159">Si es necesario, también puede obtener el valor de la dirección URL de inicio de sesión del equipo de soporte de Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="9cf75-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="9cf75-160">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9cf75-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="9cf75-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9cf75-162">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cf75-164">En hello **Mixpanel configuración** sección, haga clic en **configurar Mixpanel** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9cf75-164">On hello **Mixpanel Configuration** section, click **Configure Mixpanel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9cf75-165">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9cf75-165">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="9cf75-167">En otra ventana del explorador, inicio de sesión tooyour Mixpanel aplicación como administrador.</span><span class="sxs-lookup"><span data-stu-id="9cf75-167">In a different browser window, sign-on tooyour Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="9cf75-168">En la parte inferior de la página de hello, haga clic en hello poco **engranaje** icono en la esquina izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf75-168">On bottom of hello page, click hello little **gear** icon in hello left corner.</span></span> 
   
    ![Inicio de sesión único de Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="9cf75-170">Haga clic en hello **de seguridad de acceso** ficha y, a continuación, haga clic en **cambiar la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-170">Click hello **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Configuración de Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="9cf75-172">En hello **cambiar su certificado** página del cuadro de diálogo, haga clic en **Elegir archivo** tooupload el certificado descargado y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-172">On hello **Change your certificate** dialog page, click **Choose file** tooupload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Configuración de Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="9cf75-174">En hello cuadro de texto de dirección URL de la autenticación en hello **cambiar la dirección URL de autenticación** página de diálogo, pegar Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-174">In hello authentication URL textbox on hello **Change your authentication  URL** dialog page, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Configuración de Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="9cf75-176">Haga clic en **Done**(Listo).</span><span class="sxs-lookup"><span data-stu-id="9cf75-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="9cf75-177">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9cf75-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9cf75-178">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf75-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9cf75-179">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cf75-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cf75-180">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf75-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cf75-181">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9cf75-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9cf75-183">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf75-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf75-184">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9cf75-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cf75-186">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cf75-188">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf75-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cf75-190">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9cf75-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cf75-192">a.</span><span class="sxs-lookup"><span data-stu-id="9cf75-192">a.</span></span> <span data-ttu-id="9cf75-193">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cf75-194">b.</span><span class="sxs-lookup"><span data-stu-id="9cf75-194">b.</span></span> <span data-ttu-id="9cf75-195">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cf75-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cf75-196">c.</span><span class="sxs-lookup"><span data-stu-id="9cf75-196">c.</span></span> <span data-ttu-id="9cf75-197">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9cf75-198">d.</span><span class="sxs-lookup"><span data-stu-id="9cf75-198">d.</span></span> <span data-ttu-id="9cf75-199">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="9cf75-200">Creación de un usuario de prueba de Mixpanel</span><span class="sxs-lookup"><span data-stu-id="9cf75-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="9cf75-201">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Mixpanel toocreate.</span><span class="sxs-lookup"><span data-stu-id="9cf75-201">hello objective of this section is toocreate a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="9cf75-202">Inicie sesión en tooyour Mixpanel sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="9cf75-202">Sign on tooyour Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="9cf75-203">En hello parte inferior de la página de hello, haga clic en Hola engranaje poco situado en Hola de hello esquina izquierda tooopen **configuración** ventana.</span><span class="sxs-lookup"><span data-stu-id="9cf75-203">On hello bottom of hello page, click hello little gear button on hello left corner tooopen hello **Settings** window.</span></span>

3. <span data-ttu-id="9cf75-204">Haga clic en hello **equipo** ficha.</span><span class="sxs-lookup"><span data-stu-id="9cf75-204">Click hello **Team** tab.</span></span>

4. <span data-ttu-id="9cf75-205">Hola **miembro del equipo** cuadro de texto, escriba la dirección de correo electrónico de Bárbara en hello Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf75-205">In hello **team member** textbox, type Britta's email address in hello Azure.</span></span>
   
    ![Configuración de Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="9cf75-207">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="9cf75-208">Hola usuario obtendrá un tooset de correo electrónico de perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf75-208">hello user will get an email tooset up hello profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9cf75-209">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf75-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9cf75-210">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMixpanel.</span><span class="sxs-lookup"><span data-stu-id="9cf75-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMixpanel.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9cf75-212">**tooassign Britta Simon tooMixpanel, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf75-212">**tooassign Britta Simon tooMixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf75-213">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9cf75-215">En la lista de aplicaciones de hello, seleccione **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-215">In hello applications list, select **Mixpanel**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="9cf75-217">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9cf75-219">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-219">Click **Add** button.</span></span> <span data-ttu-id="9cf75-220">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9cf75-222">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf75-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cf75-223">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cf75-224">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9cf75-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cf75-225">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9cf75-225">Testing single sign-on</span></span>

<span data-ttu-id="9cf75-226">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9cf75-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9cf75-227">Al hacer clic en icono de Mixpanel Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Mixpanel aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cf75-227">When you click hello Mixpanel tile in hello Access Panel, you should get automatically signed-on tooyour Mixpanel application.</span></span>
<span data-ttu-id="9cf75-228">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9cf75-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cf75-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9cf75-229">Additional resources</span></span>

* [<span data-ttu-id="9cf75-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cf75-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cf75-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cf75-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

