---
title: "Tutorial: Integración de Azure Active Directory con ITRP | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="9bae6-103">Tutorial: Integración de Azure Active Directory con ITRP</span><span class="sxs-lookup"><span data-stu-id="9bae6-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="9bae6-104">En este tutorial, aprenderá cómo toointegrate ITRP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9bae6-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9bae6-105">Integración ITRP con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9bae6-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9bae6-106">Puede controlar en Azure AD que tenga acceso tooITRP</span><span class="sxs-lookup"><span data-stu-id="9bae6-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="9bae6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooITRP (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bae6-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9bae6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9bae6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9bae6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9bae6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bae6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9bae6-110">Prerequisites</span></span>

<span data-ttu-id="9bae6-111">integración de Azure AD con ITRP tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9bae6-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="9bae6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bae6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9bae6-113">Una suscripción habilitada para el inicio de sesión único en ITRP</span><span class="sxs-lookup"><span data-stu-id="9bae6-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9bae6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9bae6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9bae6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9bae6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9bae6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9bae6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9bae6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bae6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9bae6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9bae6-118">Scenario description</span></span>
<span data-ttu-id="9bae6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9bae6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9bae6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9bae6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9bae6-121">Agregar ITRP desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9bae6-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="9bae6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bae6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="9bae6-123">Agregar ITRP desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9bae6-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="9bae6-124">integración de hello tooconfigure de ITRP en tooAzure AD, deberá tooadd ITRP de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9bae6-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9bae6-125">**tooadd ITRP de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bae6-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bae6-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9bae6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9bae6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9bae6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9bae6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9bae6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9bae6-133">En el cuadro de búsqueda de hello, escriba **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-133">In hello search box, type **ITRP**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="9bae6-135">En el panel de resultados de hello, seleccione **ITRP**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9bae6-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9bae6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bae6-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="9bae6-138">En esta sección se configura y prueba el inicio de sesión único de Azure AD con ITRP con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9bae6-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9bae6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ITRP es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bae6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="9bae6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ITRP debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9bae6-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="9bae6-141">En ITRP, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bae6-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9bae6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con ITRP, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9bae6-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9bae6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9bae6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9bae6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9bae6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9bae6-145">**[Usuario de prueba de la creación de un ITRP](#creating-an-itrp-test-user)**  -toohave un equivalente de Britta Simon en ITRP que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9bae6-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9bae6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9bae6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9bae6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9bae6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9bae6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bae6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9bae6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de ITRP.</span><span class="sxs-lookup"><span data-stu-id="9bae6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="9bae6-150">**inicio de sesión único en tooconfigure Azure AD con ITRP, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bae6-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bae6-151">En el portal de Azure, en Hola Hola **ITRP** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9bae6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9bae6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="9bae6-155">En hello **ITRP dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9bae6-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="9bae6-157">a.</span><span class="sxs-lookup"><span data-stu-id="9bae6-157">a.</span></span> <span data-ttu-id="9bae6-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="9bae6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="9bae6-159">b.</span><span class="sxs-lookup"><span data-stu-id="9bae6-159">b.</span></span> <span data-ttu-id="9bae6-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="9bae6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9bae6-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9bae6-161">These values are not real.</span></span> <span data-ttu-id="9bae6-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="9bae6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9bae6-163">Póngase en contacto con [equipo de soporte técnico de cliente de ITRP](https://www.itrp.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9bae6-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="9bae6-164">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="9bae6-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="9bae6-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9bae6-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9bae6-168">En hello **configuración de ITRP** sección, haga clic en **configurar ITRP** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9bae6-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9bae6-169">Hola copia **SAML Single Sign-On dirección URL del servicio y la dirección URL de cierre de sesión** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9bae6-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="9bae6-171">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía ITRP tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="9bae6-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="9bae6-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="9bae6-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="9bae6-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="9bae6-174">En el panel de navegación izquierdo de hello, seleccione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="9bae6-175">![Inicio de sesión único](./media/active-directory-saas-itrp-tutorial/ic775571.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="9bae6-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="9bae6-176">Hola Single Sign-On de la sección de configuración, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9bae6-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9bae6-177">![Inicio de sesión único](./media/active-directory-saas-itrp-tutorial/ic775572.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="9bae6-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="9bae6-178">![Inicio de sesión único](./media/active-directory-saas-itrp-tutorial/ic775573.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="9bae6-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="9bae6-179">a.</span><span class="sxs-lookup"><span data-stu-id="9bae6-179">a.</span></span> <span data-ttu-id="9bae6-180">Hacer clic en **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-180">Click **Enable**.</span></span>

    <span data-ttu-id="9bae6-181">b.</span><span class="sxs-lookup"><span data-stu-id="9bae6-181">b.</span></span> <span data-ttu-id="9bae6-182">En **remoto registro URL de cierre de** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bae6-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9bae6-183">c.</span><span class="sxs-lookup"><span data-stu-id="9bae6-183">c.</span></span> <span data-ttu-id="9bae6-184">En **dirección URL SSO SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bae6-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9bae6-185">d.In **huella digital de certificado** cuadro de texto, pegue hello **huella digital** valor de certificado en el que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bae6-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="9bae6-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9bae6-187">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9bae6-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9bae6-188">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9bae6-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9bae6-189">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9bae6-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9bae6-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bae6-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="9bae6-191">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9bae6-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9bae6-193">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bae6-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bae6-194">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9bae6-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9bae6-196">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9bae6-198">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bae6-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9bae6-200">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9bae6-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9bae6-202">a.</span><span class="sxs-lookup"><span data-stu-id="9bae6-202">a.</span></span> <span data-ttu-id="9bae6-203">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9bae6-204">b.</span><span class="sxs-lookup"><span data-stu-id="9bae6-204">b.</span></span> <span data-ttu-id="9bae6-205">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9bae6-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9bae6-206">c.</span><span class="sxs-lookup"><span data-stu-id="9bae6-206">c.</span></span> <span data-ttu-id="9bae6-207">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9bae6-208">d.</span><span class="sxs-lookup"><span data-stu-id="9bae6-208">d.</span></span> <span data-ttu-id="9bae6-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="9bae6-210">Creación de un usuario de prueba de ITRP</span><span class="sxs-lookup"><span data-stu-id="9bae6-210">Creating an ITRP test user</span></span>

<span data-ttu-id="9bae6-211">toolog de los usuarios de Azure AD tooenable en tooITRP, se les deben aprovisionar en tooITRP.</span><span class="sxs-lookup"><span data-stu-id="9bae6-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="9bae6-212">En caso de hello de ITRP, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9bae6-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="9bae6-213">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bae6-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bae6-214">Inicie sesión en tooyour **ITRP** inquilino.</span><span class="sxs-lookup"><span data-stu-id="9bae6-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="9bae6-215">En la barra de herramientas de hello en la parte superior de hello, haga clic en **registros**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="9bae6-216">![Administración](./media/active-directory-saas-itrp-tutorial/ic775575.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="9bae6-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="9bae6-217">En el menú emergente de hello, seleccione **personas**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="9bae6-218">![Personas](./media/active-directory-saas-itrp-tutorial/ic775587.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="9bae6-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="9bae6-219">Haga clic en **Agregar nueva persona** (“+”).</span><span class="sxs-lookup"><span data-stu-id="9bae6-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="9bae6-220">![Administración](./media/active-directory-saas-itrp-tutorial/ic775576.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="9bae6-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="9bae6-221">En el cuadro de diálogo de agregar nueva persona hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9bae6-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="9bae6-222">![Usuario](./media/active-directory-saas-itrp-tutorial/ic775577.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="9bae6-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="9bae6-223">a.</span><span class="sxs-lookup"><span data-stu-id="9bae6-223">a.</span></span> <span data-ttu-id="9bae6-224">Hola de tipo **nombre**, **correo electrónico** de una cuenta válida de AAD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9bae6-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="9bae6-225">b.</span><span class="sxs-lookup"><span data-stu-id="9bae6-225">b.</span></span> <span data-ttu-id="9bae6-226">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="9bae6-227">Puede usar cualquier otra ITRP usuario cuenta herramienta de creación o las API proporcionadas por ITRP tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="9bae6-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9bae6-228">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bae6-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9bae6-229">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooITRP.</span><span class="sxs-lookup"><span data-stu-id="9bae6-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9bae6-231">**tooassign Britta Simon tooITRP, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bae6-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bae6-232">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9bae6-234">En la lista de aplicaciones de hello, seleccione **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-234">In hello applications list, select **ITRP**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="9bae6-236">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9bae6-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-238">Click **Add** button.</span></span> <span data-ttu-id="9bae6-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9bae6-241">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bae6-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9bae6-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9bae6-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9bae6-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9bae6-244">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9bae6-244">Testing single sign-on</span></span>

<span data-ttu-id="9bae6-245">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9bae6-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9bae6-246">Al hacer clic en hello ITRP disponer en mosaico en el Panel de acceso de hello, deberá obtener la aplicación de ITRP tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="9bae6-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="9bae6-247">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9bae6-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9bae6-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9bae6-248">Additional resources</span></span>

* [<span data-ttu-id="9bae6-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9bae6-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9bae6-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9bae6-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

