---
title: "Tutorial: Integración de Azure Active Directory con OpsGenie | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="3afb6-103">Tutorial: Integración de Azure Active Directory con OpsGenie</span><span class="sxs-lookup"><span data-stu-id="3afb6-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="3afb6-104">En este tutorial, aprenderá cómo toointegrate OpsGenie con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3afb6-104">In this tutorial, you learn how toointegrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3afb6-105">Integración OpsGenie con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3afb6-105">Integrating OpsGenie with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3afb6-106">Puede controlar en Azure AD que tenga acceso tooOpsGenie</span><span class="sxs-lookup"><span data-stu-id="3afb6-106">You can control in Azure AD who has access tooOpsGenie</span></span>
- <span data-ttu-id="3afb6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooOpsGenie (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3afb6-107">You can enable your users tooautomatically get signed-on tooOpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3afb6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3afb6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3afb6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3afb6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3afb6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3afb6-110">Prerequisites</span></span>

<span data-ttu-id="3afb6-111">integración de Azure AD con OpsGenie tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3afb6-111">tooconfigure Azure AD integration with OpsGenie, you need hello following items:</span></span>

- <span data-ttu-id="3afb6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3afb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3afb6-113">Una suscripción habilitada para inicio de sesión único en Pluralsight</span><span class="sxs-lookup"><span data-stu-id="3afb6-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3afb6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3afb6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3afb6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3afb6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3afb6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3afb6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3afb6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3afb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3afb6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3afb6-118">Scenario description</span></span>
<span data-ttu-id="3afb6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3afb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3afb6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3afb6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3afb6-121">Agregar OpsGenie desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3afb6-121">Adding OpsGenie from hello gallery</span></span>
2. <span data-ttu-id="3afb6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3afb6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-hello-gallery"></a><span data-ttu-id="3afb6-123">Agregar OpsGenie desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3afb6-123">Adding OpsGenie from hello gallery</span></span>
<span data-ttu-id="3afb6-124">integración de hello tooconfigure de OpsGenie en Azure AD, deberá tooadd OpsGenie de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3afb6-124">tooconfigure hello integration of OpsGenie into Azure AD, you need tooadd OpsGenie from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3afb6-125">**tooadd OpsGenie de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3afb6-125">**tooadd OpsGenie from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3afb6-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3afb6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3afb6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3afb6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3afb6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3afb6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3afb6-133">En el cuadro de búsqueda de hello, escriba **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-133">In hello search box, type **OpsGenie**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="3afb6-135">En el panel de resultados de hello, seleccione **OpsGenie**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3afb6-135">In hello results panel, select **OpsGenie**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3afb6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3afb6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3afb6-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con OpsGenie con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3afb6-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3afb6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en OpsGenie es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3afb6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OpsGenie is tooa user in Azure AD.</span></span> <span data-ttu-id="3afb6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en OpsGenie debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3afb6-140">In other words, a link relationship between an Azure AD user and hello related user in OpsGenie needs toobe established.</span></span>

<span data-ttu-id="3afb6-141">En OpsGenie, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3afb6-141">In OpsGenie, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3afb6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con OpsGenie, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3afb6-142">tooconfigure and test Azure AD single sign-on with OpsGenie, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3afb6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3afb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3afb6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3afb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3afb6-145">**[Crear un usuario de prueba OpsGenie](#creating-a-opsgenie-test-user)**  -toohave un equivalente de Britta Simon en OpsGenie que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3afb6-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - toohave a counterpart of Britta Simon in OpsGenie that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3afb6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3afb6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3afb6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3afb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3afb6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3afb6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3afb6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="3afb6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="3afb6-150">**inicio de sesión único en Azure AD tooconfigure con OpsGenie, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3afb6-150">**tooconfigure Azure AD single sign-on with OpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="3afb6-151">En el portal de Azure, en Hola Hola **OpsGenie** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-151">In hello Azure portal, on hello **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3afb6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3afb6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="3afb6-155">En hello **OpsGenie dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3afb6-155">On hello **OpsGenie Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="3afb6-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="3afb6-157">In hello **Sign-on URL** textbox, type hello URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="3afb6-158">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3afb6-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="3afb6-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3afb6-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3afb6-162">En hello **OpsGenie configuración** sección, haga clic en **configurar OpsGenie** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3afb6-162">On hello **OpsGenie Configuration** section, click **Configure OpsGenie** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3afb6-163">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3afb6-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="3afb6-165">Abra otra instancia del explorador y, a continuación, inicie sesión en tooOpsGenie como administrador.</span><span class="sxs-lookup"><span data-stu-id="3afb6-165">Open another browser instance, and then log-in tooOpsGenie as an administrator.</span></span>

8. <span data-ttu-id="3afb6-166">Haga clic en **configuración**y, a continuación, haga clic en hello **Single Sign On** ficha.</span><span class="sxs-lookup"><span data-stu-id="3afb6-166">Click **Settings**, and then click hello **Single Sign On** tab.</span></span>
   
    ![Inicio de sesión único de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="3afb6-168">Seleccione tooenable SSO, **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-168">tooenable SSO, select **Enabled**.</span></span>
   
    ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="3afb6-170">Hola **proveedor** sección, haga clic en hello **Azure Active Directory** ficha.</span><span class="sxs-lookup"><span data-stu-id="3afb6-170">In hello **Provider** section, click hello **Azure Active Directory** tab.</span></span>
   
    ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="3afb6-172">En la página de diálogo de hello Azure Active Directory, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3afb6-172">On hello Azure Active Directory dialog page, perform hello following steps:</span></span>
   
    ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="3afb6-174">a.</span><span class="sxs-lookup"><span data-stu-id="3afb6-174">a.</span></span> <span data-ttu-id="3afb6-175">Pegar **único inicio de sesión en dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **punto de conexión de SAML 2.0** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3afb6-175">Paste **Single Sign On Service URL**, which you have copied from hello Azure portal into hello **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="3afb6-176">b.</span><span class="sxs-lookup"><span data-stu-id="3afb6-176">b.</span></span> <span data-ttu-id="3afb6-177">Abra el certificado codificado en base 64 descargado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo en hello **X.500 certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3afb6-177">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="3afb6-178">c.</span><span class="sxs-lookup"><span data-stu-id="3afb6-178">c.</span></span> <span data-ttu-id="3afb6-179">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3afb6-180">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3afb6-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3afb6-181">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3afb6-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3afb6-182">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3afb6-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3afb6-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3afb6-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="3afb6-184">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3afb6-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3afb6-186">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3afb6-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3afb6-187">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3afb6-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3afb6-189">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3afb6-191">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3afb6-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3afb6-193">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3afb6-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3afb6-195">a.</span><span class="sxs-lookup"><span data-stu-id="3afb6-195">a.</span></span> <span data-ttu-id="3afb6-196">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3afb6-197">b.</span><span class="sxs-lookup"><span data-stu-id="3afb6-197">b.</span></span> <span data-ttu-id="3afb6-198">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3afb6-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3afb6-199">c.</span><span class="sxs-lookup"><span data-stu-id="3afb6-199">c.</span></span> <span data-ttu-id="3afb6-200">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3afb6-201">d.</span><span class="sxs-lookup"><span data-stu-id="3afb6-201">d.</span></span> <span data-ttu-id="3afb6-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="3afb6-203">Creación de un usuario de prueba de OpsGenie</span><span class="sxs-lookup"><span data-stu-id="3afb6-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="3afb6-204">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en OpsGenie toocreate.</span><span class="sxs-lookup"><span data-stu-id="3afb6-204">hello objective of this section is toocreate a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="3afb6-205">En una ventana del explorador web, inicie sesión en el inquilino de OpsGenie como administrador.</span><span class="sxs-lookup"><span data-stu-id="3afb6-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="3afb6-206">Navegue tooUsers lista haciendo clic en **usuario** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="3afb6-206">Navigate tooUsers list by clicking **User** in left panel.</span></span>
   
   ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="3afb6-208">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-208">Click **Add User**.</span></span>

4. <span data-ttu-id="3afb6-209">En hello **Agregar usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3afb6-209">On hello **Add User** dialog, perform hello following steps:</span></span>
   
   ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="3afb6-211">a.</span><span class="sxs-lookup"><span data-stu-id="3afb6-211">a.</span></span> <span data-ttu-id="3afb6-212">Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de tipo hello de BrittaSimon tratada en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3afb6-212">In hello **Email** textbox, type hello email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="3afb6-213">b.</span><span class="sxs-lookup"><span data-stu-id="3afb6-213">b.</span></span> <span data-ttu-id="3afb6-214">Hola **nombre completo** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-214">In hello **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="3afb6-215">c.</span><span class="sxs-lookup"><span data-stu-id="3afb6-215">c.</span></span> <span data-ttu-id="3afb6-216">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="3afb6-217">Britta recibirá un correo electrónico con instrucciones sobre cómo configurar su perfil.</span><span class="sxs-lookup"><span data-stu-id="3afb6-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3afb6-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3afb6-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3afb6-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooOpsGenie.</span><span class="sxs-lookup"><span data-stu-id="3afb6-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOpsGenie.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3afb6-221">**tooassign Britta Simon tooOpsGenie, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3afb6-221">**tooassign Britta Simon tooOpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="3afb6-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3afb6-224">En la lista de aplicaciones de hello, seleccione **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-224">In hello applications list, select **OpsGenie**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="3afb6-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3afb6-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-228">Click **Add** button.</span></span> <span data-ttu-id="3afb6-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3afb6-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3afb6-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3afb6-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3afb6-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3afb6-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3afb6-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3afb6-234">Testing single sign-on</span></span>

<span data-ttu-id="3afb6-235">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3afb6-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="3afb6-236">Al hacer clic en icono de OpsGenie Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour OpsGenie aplicación.</span><span class="sxs-lookup"><span data-stu-id="3afb6-236">When you click hello OpsGenie tile in hello Access Panel, you should get automatically signed-on tooyour OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3afb6-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3afb6-237">Additional resources</span></span>

* [<span data-ttu-id="3afb6-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3afb6-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3afb6-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3afb6-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

