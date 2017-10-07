---
title: "Tutorial: integración de Azure Active Directory con Intacct | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="cf524-103">Tutorial: integración de Azure Active Directory con Intacct</span><span class="sxs-lookup"><span data-stu-id="cf524-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="cf524-104">En este tutorial, aprenderá cómo toointegrate Intacct con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf524-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf524-105">Integración Intacct con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cf524-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cf524-106">Puede controlar en Azure AD que tenga acceso tooIntacct</span><span class="sxs-lookup"><span data-stu-id="cf524-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="cf524-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooIntacct (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf524-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf524-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cf524-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cf524-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf524-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf524-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cf524-110">Prerequisites</span></span>

<span data-ttu-id="cf524-111">integración de Azure AD con Intacct tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cf524-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="cf524-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf524-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf524-113">Una suscripción habilitada para el inicio de sesión único en Intacct</span><span class="sxs-lookup"><span data-stu-id="cf524-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf524-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cf524-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf524-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cf524-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf524-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cf524-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf524-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf524-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf524-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cf524-118">Scenario description</span></span>
<span data-ttu-id="cf524-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cf524-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf524-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cf524-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf524-121">Agregar Intacct desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cf524-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="cf524-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf524-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="cf524-123">Agregar Intacct desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cf524-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="cf524-124">integración de hello tooconfigure de Intacct en Azure AD, deberá tooadd Intacct de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cf524-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cf524-125">**tooadd Intacct de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cf524-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf524-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cf524-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf524-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cf524-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cf524-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cf524-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cf524-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cf524-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cf524-133">En el cuadro de búsqueda de hello, escriba **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="cf524-133">In hello search box, type **Intacct**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="cf524-135">En el panel de resultados de hello, seleccione **Intacct**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cf524-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf524-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf524-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf524-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Intacct con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cf524-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf524-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Intacct es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf524-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="cf524-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Intacct debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cf524-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="cf524-141">En Intacct, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf524-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cf524-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Intacct, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cf524-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cf524-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cf524-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cf524-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf524-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf524-145">**[Creación de un usuario de prueba de Intacct](#creating-an-intacct-test-user) ** -toohave un equivalente de Britta Simon en Intacct que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="cf524-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf524-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cf524-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf524-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cf524-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf524-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf524-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf524-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Intacct.</span><span class="sxs-lookup"><span data-stu-id="cf524-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="cf524-150">**inicio de sesión único en Azure AD tooconfigure con Intacct, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cf524-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf524-151">En el portal de Azure, en Hola Hola **Intacct** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cf524-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cf524-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cf524-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="cf524-155">En hello **Intacct dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cf524-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="cf524-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="cf524-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="cf524-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="cf524-158">This value is not real.</span></span> <span data-ttu-id="cf524-159">Actualizar este valor con la dirección URL de respuesta real Hola.</span><span class="sxs-lookup"><span data-stu-id="cf524-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="cf524-160">Póngase en contacto con [equipo de soporte técnico de Intacct](https://us.intacct.com/support) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="cf524-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="cf524-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cf524-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="cf524-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cf524-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cf524-165">En hello **configuración de Intacct** sección, haga clic en **configurar Intacct** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="cf524-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cf524-166">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="cf524-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="cf524-168">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía Intacct tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="cf524-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="cf524-169">Haga clic en hello **empresa** ficha y, a continuación, haga clic en **información de la empresa**.</span><span class="sxs-lookup"><span data-stu-id="cf524-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="cf524-170">![Compañía](./media/active-directory-saas-intacct-tutorial/ic790037.png "Compañía")</span><span class="sxs-lookup"><span data-stu-id="cf524-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="cf524-171">Haga clic en hello **seguridad** ficha y, a continuación, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="cf524-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="cf524-172">![Seguridad](./media/active-directory-saas-intacct-tutorial/ic790038.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="cf524-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="cf524-173">Hola **único (SSO) de inicio de sesión** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cf524-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="cf524-174">![Inicio de sesión único](./media/active-directory-saas-intacct-tutorial/ic790039.png "inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="cf524-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="cf524-175">a.</span><span class="sxs-lookup"><span data-stu-id="cf524-175">a.</span></span> <span data-ttu-id="cf524-176">Seleccione **Habilitar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cf524-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="cf524-177">b.</span><span class="sxs-lookup"><span data-stu-id="cf524-177">b.</span></span> <span data-ttu-id="cf524-178">En **Tipo de proveedor de identidades**, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="cf524-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="cf524-179">c.</span><span class="sxs-lookup"><span data-stu-id="cf524-179">c.</span></span> <span data-ttu-id="cf524-180">En **dirección URL del emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf524-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="cf524-181">d.</span><span class="sxs-lookup"><span data-stu-id="cf524-181">d.</span></span> <span data-ttu-id="cf524-182">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf524-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cf524-183">e.</span><span class="sxs-lookup"><span data-stu-id="cf524-183">e.</span></span> <span data-ttu-id="cf524-184">Abra su **base-64** codificado certificado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado** cuadro.</span><span class="sxs-lookup"><span data-stu-id="cf524-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="cf524-185">f.</span><span class="sxs-lookup"><span data-stu-id="cf524-185">f.</span></span> <span data-ttu-id="cf524-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cf524-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cf524-187">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cf524-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cf524-188">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cf524-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cf524-189">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf524-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf524-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf524-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf524-191">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cf524-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cf524-193">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cf524-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf524-194">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cf524-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf524-196">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cf524-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf524-198">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf524-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf524-200">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cf524-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf524-202">a.</span><span class="sxs-lookup"><span data-stu-id="cf524-202">a.</span></span> <span data-ttu-id="cf524-203">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf524-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf524-204">b.</span><span class="sxs-lookup"><span data-stu-id="cf524-204">b.</span></span> <span data-ttu-id="cf524-205">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf524-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf524-206">c.</span><span class="sxs-lookup"><span data-stu-id="cf524-206">c.</span></span> <span data-ttu-id="cf524-207">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cf524-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cf524-208">d.</span><span class="sxs-lookup"><span data-stu-id="cf524-208">d.</span></span> <span data-ttu-id="cf524-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cf524-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="cf524-210">Creación de un usuario de prueba de Intacct</span><span class="sxs-lookup"><span data-stu-id="cf524-210">Creating an Intacct test user</span></span>

<span data-ttu-id="cf524-211">tooset configurar usuarios de Azure AD para que puedan iniciar sesión en tooIntacct, se les deben aprovisionar en Intacct.</span><span class="sxs-lookup"><span data-stu-id="cf524-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="cf524-212">Para Intacct, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="cf524-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="cf524-213">**cuentas de usuario de tooprovision, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cf524-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf524-214">Inicie sesión en tooyour **Intacct** inquilino.</span><span class="sxs-lookup"><span data-stu-id="cf524-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="cf524-215">Haga clic en hello **empresa** ficha y, a continuación, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cf524-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="cf524-216">![Usuarios](./media/active-directory-saas-intacct-tutorial/ic790041.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="cf524-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="cf524-217">Haga clic en hello **agregar** ficha.</span><span class="sxs-lookup"><span data-stu-id="cf524-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="cf524-218">![Agregar](./media/active-directory-saas-intacct-tutorial/ic790042.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="cf524-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="cf524-219">Hola **información del usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cf524-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="cf524-220">![Información del usuario](./media/active-directory-saas-intacct-tutorial/ic790043.png "Información del usuario")</span><span class="sxs-lookup"><span data-stu-id="cf524-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="cf524-221">a.</span><span class="sxs-lookup"><span data-stu-id="cf524-221">a.</span></span> <span data-ttu-id="cf524-222">Escriba hello **Id. de usuario**, hello **apellidos**, **nombre**, hello **dirección de correo electrónico**, hello **título**, hello y **teléfono** de una cuenta de Azure AD que quiera tooprovision en hello **información del usuario** sección.</span><span class="sxs-lookup"><span data-stu-id="cf524-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="cf524-223">b.</span><span class="sxs-lookup"><span data-stu-id="cf524-223">b.</span></span> <span data-ttu-id="cf524-224">Seleccione hello **privilegios de administrador** de una cuenta de Azure AD que desea tooprovision.</span><span class="sxs-lookup"><span data-stu-id="cf524-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="cf524-225">c.</span><span class="sxs-lookup"><span data-stu-id="cf524-225">c.</span></span> <span data-ttu-id="cf524-226">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cf524-226">Click **Save**.</span></span> <span data-ttu-id="cf524-227">titular de la cuenta de Hello Azure AD recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="cf524-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="cf524-228">cuentas de usuario de Azure AD tooprovision, puede usar otra herramienta de creación de cuentas de usuario de Intacct o las API proporcionadas por Intacct.</span><span class="sxs-lookup"><span data-stu-id="cf524-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cf524-229">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf524-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cf524-230">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooIntacct.</span><span class="sxs-lookup"><span data-stu-id="cf524-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cf524-232">**tooassign Britta Simon tooIntacct, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cf524-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf524-233">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cf524-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cf524-235">En la lista de aplicaciones de hello, seleccione **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="cf524-235">In hello applications list, select **Intacct**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="cf524-237">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cf524-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cf524-239">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cf524-239">Click **Add** button.</span></span> <span data-ttu-id="cf524-240">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cf524-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cf524-242">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf524-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cf524-243">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cf524-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf524-244">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cf524-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf524-245">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cf524-245">Testing single sign-on</span></span>

<span data-ttu-id="cf524-246">En esta sección, probará la configuración de inicio de sesión única de Azure AD mediante el uso de hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cf524-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="cf524-247">Al hacer clic en icono de Intacct Hola Hola Panel de acceso, debería firmar automáticamente en tooyour Intacct aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf524-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf524-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cf524-248">Additional resources</span></span>

* [<span data-ttu-id="cf524-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf524-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf524-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf524-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

