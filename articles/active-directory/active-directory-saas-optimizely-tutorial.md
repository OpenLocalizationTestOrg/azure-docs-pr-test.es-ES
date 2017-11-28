---
title: "Tutorial: integración de Azure Active Directory con Optimizely | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="cc53f-103">Tutorial: integración de Azure Active Directory con Optimizely</span><span class="sxs-lookup"><span data-stu-id="cc53f-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="cc53f-104">En este tutorial, aprenderá cómo toointegrate Optimizely con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc53f-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc53f-105">Integración Optimizely con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cc53f-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc53f-106">Puede controlar en Azure AD que tenga acceso tooOptimizely</span><span class="sxs-lookup"><span data-stu-id="cc53f-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="cc53f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooOptimizely (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc53f-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc53f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cc53f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc53f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc53f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc53f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cc53f-110">Prerequisites</span></span>

<span data-ttu-id="cc53f-111">integración de Azure AD con Optimizely tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cc53f-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="cc53f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc53f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc53f-113">Una suscripción habilitada para el inicio de sesión único en Optimizely</span><span class="sxs-lookup"><span data-stu-id="cc53f-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc53f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cc53f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc53f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cc53f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc53f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cc53f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc53f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc53f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc53f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cc53f-118">Scenario description</span></span>
<span data-ttu-id="cc53f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cc53f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc53f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cc53f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc53f-121">Agregar Optimizely desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc53f-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="cc53f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc53f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="cc53f-123">Agregar Optimizely desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc53f-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="cc53f-124">integración de hello tooconfigure de Optimizely en Azure AD, deberá tooadd Optimizely de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cc53f-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc53f-125">**tooadd Optimizely de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc53f-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc53f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cc53f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc53f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc53f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cc53f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cc53f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cc53f-133">En el cuadro de búsqueda de hello, escriba **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-133">In hello search box, type **Optimizely**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="cc53f-135">En el panel de resultados de hello, seleccione **Optimizely**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc53f-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc53f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc53f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc53f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Optimizely con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc53f-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc53f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Optimizely es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc53f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="cc53f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Optimizely debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cc53f-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="cc53f-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Optimizely.</span><span class="sxs-lookup"><span data-stu-id="cc53f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="cc53f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Optimizely, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cc53f-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc53f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cc53f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc53f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc53f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc53f-145">**[Creación de un usuario de prueba Optimizely](#creating-an-optimizely-test-user)**  -toohave un equivalente de Britta Simon en Optimizely que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="cc53f-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc53f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cc53f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc53f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cc53f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc53f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc53f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc53f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Optimizely.</span><span class="sxs-lookup"><span data-stu-id="cc53f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="cc53f-150">**inicio de sesión único en Azure AD tooconfigure con Optimizely, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc53f-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc53f-151">En el portal de Azure, en Hola Hola **Optimizely** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cc53f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cc53f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="cc53f-155">En hello **Optimizely dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cc53f-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="cc53f-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc53f-157">a.</span></span> <span data-ttu-id="cc53f-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="cc53f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="cc53f-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc53f-159">b.</span></span> <span data-ttu-id="cc53f-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="cc53f-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc53f-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="cc53f-161">These values are not hello real.</span></span> <span data-ttu-id="cc53f-162">Valor de hello actualizará con URL de inicio de sesión real de Hola y el identificador, que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="cc53f-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="cc53f-163">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cc53f-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="cc53f-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cc53f-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc53f-167">En hello **Optimizely configuración** sección, haga clic en **configurar Optimizely** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="cc53f-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc53f-168">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="cc53f-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="cc53f-170">tooconfigure inicio de sesión único en **Optimizely** en paralelo, póngase en contacto con su administrador de cuentas de Optimizely y proporcionar Hola descargado **certificado (Base64)**, y **SAML Single Sign-On dirección URL del servicio** .</span><span class="sxs-lookup"><span data-stu-id="cc53f-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="cc53f-171">En correo electrónico de respuesta tooyour, Optimizely proporciona hello y hello en URL de sesión (SSO iniciado por el SP) valores de identificador (ID de entidad de proveedor de servicio).</span><span class="sxs-lookup"><span data-stu-id="cc53f-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="cc53f-172">a.</span><span class="sxs-lookup"><span data-stu-id="cc53f-172">a.</span></span> <span data-ttu-id="cc53f-173">Hola copia **dirección URL de SSO iniciado por el SP** proporcionado por Optimizely y péguelo en hello **dirección URL de inicio de sesión** en el cuadro de texto **Optimizely dominio y las direcciones URL** sección en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cc53f-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="cc53f-174">b.</span><span class="sxs-lookup"><span data-stu-id="cc53f-174">b.</span></span> <span data-ttu-id="cc53f-175">Hola copia **Id. de entidad de proveedor de servicio** proporcionado por Optimizely y péguelo en hello **identificador** en el cuadro de texto **Optimizely dominio y las direcciones URL** sección en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cc53f-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="cc53f-176">En otra ventana del explorador, inicio de sesión tooyour Optimizely aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc53f-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="cc53f-177">Haga clic en cuenta que el nombre en la parte superior de hello esquina derecha y, a continuación, **configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Inicio de sesión único de Azure AD ](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="cc53f-179">En la pestaña de la cuenta de hello, casilla hello **habilitar SSO** en el inicio de sesión único en hello **Introducción** sección.</span><span class="sxs-lookup"><span data-stu-id="cc53f-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Inicio de sesión único de Azure AD ](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="cc53f-181">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="cc53f-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="cc53f-182">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cc53f-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc53f-183">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cc53f-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc53f-184">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc53f-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc53f-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc53f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc53f-186">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cc53f-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cc53f-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc53f-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc53f-189">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cc53f-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc53f-191">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc53f-193">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc53f-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc53f-195">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cc53f-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc53f-197">a.</span><span class="sxs-lookup"><span data-stu-id="cc53f-197">a.</span></span> <span data-ttu-id="cc53f-198">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc53f-199">b.</span><span class="sxs-lookup"><span data-stu-id="cc53f-199">b.</span></span> <span data-ttu-id="cc53f-200">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc53f-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="cc53f-201">c.</span><span class="sxs-lookup"><span data-stu-id="cc53f-201">c.</span></span> <span data-ttu-id="cc53f-202">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc53f-203">d.</span><span class="sxs-lookup"><span data-stu-id="cc53f-203">d.</span></span> <span data-ttu-id="cc53f-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="cc53f-205">Creación de un usuario de prueba de Optimizely</span><span class="sxs-lookup"><span data-stu-id="cc53f-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="cc53f-206">En esta sección, creará un usuario llamado Britta Simon en Optimizely.</span><span class="sxs-lookup"><span data-stu-id="cc53f-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="cc53f-207">En la página de inicio de hello, seleccione **colaboradores** ficha.</span><span class="sxs-lookup"><span data-stu-id="cc53f-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="cc53f-208">nuevo proyecto de colaborador del toohello tooadd, haga clic en **Colaborador nuevo**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="cc53f-210">Rellene la dirección de correo electrónico de Hola y les asigne un rol.</span><span class="sxs-lookup"><span data-stu-id="cc53f-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="cc53f-211">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-211">Click **Invite**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="cc53f-213">El usuario recibirá una invitación por correo electrónico,</span><span class="sxs-lookup"><span data-stu-id="cc53f-213">They receive an email invite.</span></span> <span data-ttu-id="cc53f-214">Con la dirección de correo electrónico de hello, tienen toolog en tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="cc53f-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc53f-215">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc53f-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc53f-216">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="cc53f-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cc53f-218">**tooassign Britta Simon tooOptimizely, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc53f-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc53f-219">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cc53f-221">En la lista de aplicaciones de hello, seleccione **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-221">In hello applications list, select **Optimizely**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="cc53f-223">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cc53f-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-225">Click **Add** button.</span></span> <span data-ttu-id="cc53f-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cc53f-228">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc53f-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc53f-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc53f-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cc53f-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc53f-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cc53f-231">Testing single sign-on</span></span>

<span data-ttu-id="cc53f-232">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cc53f-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc53f-233">Al hacer clic en icono de Optimizely Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Optimizely aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc53f-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc53f-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cc53f-234">Additional resources</span></span>

* [<span data-ttu-id="cc53f-235">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc53f-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc53f-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc53f-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

