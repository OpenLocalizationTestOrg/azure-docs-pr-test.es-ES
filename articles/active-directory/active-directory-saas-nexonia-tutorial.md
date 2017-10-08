---
title: "Tutorial: Integración de Azure Active Directory con Nexonia | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="9fa9b-103">Tutorial: Integración de Azure Active Directory con Nexonia</span><span class="sxs-lookup"><span data-stu-id="9fa9b-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="9fa9b-104">En este tutorial, aprenderá cómo toointegrate Nexonia con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fa9b-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9fa9b-105">Integración Nexonia con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9fa9b-106">Puede controlar en Azure AD que tenga acceso tooNexonia</span><span class="sxs-lookup"><span data-stu-id="9fa9b-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="9fa9b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNexonia (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa9b-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9fa9b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9fa9b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9fa9b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9fa9b-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="9fa9b-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fa9b-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9fa9b-111">Prerequisites</span></span>

<span data-ttu-id="9fa9b-112">integración de Azure AD con Nexonia tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="9fa9b-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa9b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9fa9b-114">Una suscripción habilitada para el inicio de sesión único en Nexonia</span><span class="sxs-lookup"><span data-stu-id="9fa9b-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9fa9b-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9fa9b-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9fa9b-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9fa9b-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9fa9b-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9fa9b-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9fa9b-119">Scenario description</span></span>
<span data-ttu-id="9fa9b-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9fa9b-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fa9b-122">Agregar Nexonia desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9fa9b-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="9fa9b-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa9b-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="9fa9b-124">Agregar Nexonia desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9fa9b-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="9fa9b-125">integración de hello tooconfigure de Nexonia en Azure AD, deberá tooadd Nexonia de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9fa9b-126">**tooadd Nexonia de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa9b-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9fa9b-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9fa9b-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9fa9b-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9fa9b-134">En el cuadro de búsqueda de hello, escriba **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-134">In hello search box, type **Nexonia**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="9fa9b-136">En el panel de resultados de hello, seleccione **Nexonia**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9fa9b-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa9b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9fa9b-139">En esta sección podrá configurar y probar el inicio de sesión único de Azure AD con Nexonia con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9fa9b-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9fa9b-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Nexonia es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="9fa9b-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Nexonia debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="9fa9b-142">En Nexonia, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9fa9b-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Nexonia, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9fa9b-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9fa9b-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fa9b-146">**[Crear un usuario de prueba Nexonia](#creating-a-nexonia-test-user)**  -toohave un equivalente de Britta Simon en Nexonia que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9fa9b-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fa9b-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9fa9b-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa9b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9fa9b-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Nexonia.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="9fa9b-151">Si tiene problemas de integración de hello, consulte este [vínculo](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) de guía para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="9fa9b-152">Si todavía no ha encontrado solución hello, a continuación, generar solicitud de soporte técnico de Hola desde portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="9fa9b-153">**inicio de sesión único en Azure AD tooconfigure con Nexonia, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa9b-154">En el portal de Azure, en Hola Hola **Nexonia** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9fa9b-156">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="9fa9b-158">En hello **Nexonia dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="9fa9b-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="9fa9b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9fa9b-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-161">This value is not real.</span></span> <span data-ttu-id="9fa9b-162">Actualizar este valor con la dirección URL de respuesta real Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="9fa9b-163">Póngase en contacto con [equipo de soporte técnico de Nexonia](https://nexonia.zendesk.com/hc/requests/new) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="9fa9b-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="9fa9b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9fa9b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9fa9b-168">En hello **Nexonia configuración** sección, haga clic en **configurar Nexonia** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9fa9b-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="9fa9b-171">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de Nexonia](https://nexonia.zendesk.com/hc/requests/new) y proporcionarles siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="9fa9b-172">Hola • descargado **certificado**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="9fa9b-173">• hello **Id. de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="9fa9b-174">• hello **SAML Single Sign-On dirección URL del servicio**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="9fa9b-175">• hello **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="9fa9b-176">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9fa9b-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9fa9b-177">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9fa9b-178">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9fa9b-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9fa9b-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa9b-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="9fa9b-180">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9fa9b-182">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa9b-183">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9fa9b-185">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9fa9b-187">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fa9b-189">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9fa9b-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9fa9b-191">a.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-191">a.</span></span> <span data-ttu-id="9fa9b-192">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9fa9b-193">b.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-193">b.</span></span> <span data-ttu-id="9fa9b-194">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9fa9b-195">c.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-195">c.</span></span> <span data-ttu-id="9fa9b-196">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9fa9b-197">d.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-197">d.</span></span> <span data-ttu-id="9fa9b-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="9fa9b-199">Creación de un usuario de prueba de Nexonia</span><span class="sxs-lookup"><span data-stu-id="9fa9b-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="9fa9b-200">En esta sección, creará un usuario llamado Britta Simon en Nexonia.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="9fa9b-201">Trabajar con [equipo de soporte técnico de Nexonia](https://nexonia.zendesk.com/hc/requests/new) a los usuarios de tooadd hello en la plataforma de Nexonia Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="9fa9b-202">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9fa9b-203">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa9b-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9fa9b-204">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNexonia.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9fa9b-206">**tooassign Britta Simon tooNexonia, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9fa9b-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa9b-207">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9fa9b-209">En la lista de aplicaciones de hello, seleccione **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-209">In hello applications list, select **Nexonia**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="9fa9b-211">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9fa9b-213">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-213">Click **Add** button.</span></span> <span data-ttu-id="9fa9b-214">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9fa9b-216">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9fa9b-217">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9fa9b-218">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9fa9b-219">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9fa9b-219">Testing single sign-on</span></span>

<span data-ttu-id="9fa9b-220">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9fa9b-221">Al hacer clic en icono de Nexonia Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Nexonia aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fa9b-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="9fa9b-222">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9fa9b-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fa9b-223">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9fa9b-223">Additional resources</span></span>

* [<span data-ttu-id="9fa9b-224">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fa9b-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fa9b-225">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9fa9b-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

