---
title: "Tutorial: Integración de Azure Active Directory con YouEarnedIt | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="fb8bd-103">Tutorial: Integración de Azure Active Directory con YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="fb8bd-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="fb8bd-104">En este tutorial, aprenderá cómo toointegrate YouEarnedIt con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb8bd-104">In this tutorial, you learn how toointegrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb8bd-105">Integración YouEarnedIt con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-105">Integrating YouEarnedIt with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb8bd-106">Puede controlar en Azure AD que tenga acceso tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-106">You can control in Azure AD who has access tooYouEarnedIt.</span></span>
- <span data-ttu-id="fb8bd-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooYouEarnedIt (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-107">You can enable your users tooautomatically get signed-on tooYouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fb8bd-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fb8bd-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb8bd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb8bd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb8bd-110">Prerequisites</span></span>

<span data-ttu-id="fb8bd-111">integración de Azure AD con YouEarnedIt tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-111">tooconfigure Azure AD integration with YouEarnedIt, you need hello following items:</span></span>

- <span data-ttu-id="fb8bd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb8bd-113">Una suscripción habilitada para el inicio de sesión único en YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="fb8bd-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb8bd-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb8bd-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb8bd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb8bd-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb8bd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb8bd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fb8bd-118">Scenario description</span></span>
<span data-ttu-id="fb8bd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb8bd-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb8bd-121">Agregar YouEarnedIt desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fb8bd-121">Adding YouEarnedIt from hello gallery</span></span>
2. <span data-ttu-id="fb8bd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-hello-gallery"></a><span data-ttu-id="fb8bd-123">Agregar YouEarnedIt desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fb8bd-123">Adding YouEarnedIt from hello gallery</span></span>
<span data-ttu-id="fb8bd-124">integración de hello tooconfigure de YouEarnedIt en Azure AD, deberá tooadd YouEarnedIt de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-124">tooconfigure hello integration of YouEarnedIt into Azure AD, you need tooadd YouEarnedIt from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb8bd-125">**tooadd YouEarnedIt de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb8bd-125">**tooadd YouEarnedIt from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb8bd-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="fb8bd-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb8bd-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="fb8bd-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="fb8bd-133">En el cuadro de búsqueda de hello, escriba **YouEarnedt**, seleccione **YouEarnedt** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-133">In hello search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![YouEarnedIt en la lista de resultados de Hola](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fb8bd-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8bd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fb8bd-136">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con YouEarnedIt con una usuaria de prueba llamada "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb8bd-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb8bd-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en YouEarnedIt es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in YouEarnedIt is tooa user in Azure AD.</span></span> <span data-ttu-id="fb8bd-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en YouEarnedIt debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-138">In other words, a link relationship between an Azure AD user and hello related user in YouEarnedIt needs toobe established.</span></span>

<span data-ttu-id="fb8bd-139">En YouEarnedIt, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-139">In YouEarnedIt, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fb8bd-140">tooconfigure y prueba de inicio de sesión único en Azure AD con YouEarnedIt, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-140">tooconfigure and test Azure AD single sign-on with YouEarnedIt, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb8bd-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb8bd-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb8bd-143">**[Crear un usuario de prueba YouEarnedIt](#create-a-youearnedit-test-user)**  -toohave un equivalente de Britta Simon en YouEarnedIt que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - toohave a counterpart of Britta Simon in YouEarnedIt that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb8bd-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb8bd-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fb8bd-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8bd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fb8bd-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="fb8bd-148">**inicio de sesión único en Azure AD tooconfigure con YouEarnedIt, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb8bd-148">**tooconfigure Azure AD single sign-on with YouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb8bd-149">En el portal de Azure, en Hola Hola **YouEarnedIt** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-149">In hello Azure portal, on hello **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="fb8bd-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="fb8bd-153">En hello **YouEarnedIt dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-153">On hello **YouEarnedIt Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="fb8bd-155">a.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-155">a.</span></span> <span data-ttu-id="fb8bd-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-156">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | <span data-ttu-id="fb8bd-157">Environment</span><span class="sxs-lookup"><span data-stu-id="fb8bd-157">Environment</span></span>  | <span data-ttu-id="fb8bd-158">Patrón</span><span class="sxs-lookup"><span data-stu-id="fb8bd-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="fb8bd-159">Producción</span><span class="sxs-lookup"><span data-stu-id="fb8bd-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="fb8bd-160">Espacio aislado</span><span class="sxs-lookup"><span data-stu-id="fb8bd-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="fb8bd-161">b.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-161">b.</span></span> <span data-ttu-id="fb8bd-162">Hola **identificador** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-162">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="fb8bd-163">Environment</span><span class="sxs-lookup"><span data-stu-id="fb8bd-163">Environment</span></span>  | <span data-ttu-id="fb8bd-164">Patrón</span><span class="sxs-lookup"><span data-stu-id="fb8bd-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="fb8bd-165">Producción</span><span class="sxs-lookup"><span data-stu-id="fb8bd-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="fb8bd-166">Espacio aislado</span><span class="sxs-lookup"><span data-stu-id="fb8bd-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="fb8bd-167">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-167">These values are not real.</span></span> <span data-ttu-id="fb8bd-168">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-168">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fb8bd-169">Póngase en contacto con [equipo de soporte técnico de cliente de YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) tooget these values.</span></span> 
 
4. <span data-ttu-id="fb8bd-170">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="fb8bd-172">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fb8bd-172">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb8bd-174">En hello **YouEarnedIt configuración** sección, haga clic en **configurar YouEarnedIt** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-174">On hello **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fb8bd-175">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="fb8bd-175">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="fb8bd-177">inicio de sesión único en tooconfigure en **YouEarnedIt** lado, necesita hello toosend descargado **Certificate(Base64)** y **SAML Single Sign-On dirección URL del servicio** demasiado[Equipo de soporte técnico de YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="fb8bd-177">tooconfigure single sign-on on **YouEarnedIt** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="fb8bd-178">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-178">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fb8bd-179">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="fb8bd-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb8bd-180">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb8bd-181">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb8bd-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fb8bd-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8bd-182">Create an Azure AD test user</span></span>

<span data-ttu-id="fb8bd-183">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="fb8bd-185">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb8bd-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb8bd-186">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-186">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fb8bd-188">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-188">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fb8bd-190">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-190">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fb8bd-192">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fb8bd-192">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fb8bd-194">a.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-194">a.</span></span> <span data-ttu-id="fb8bd-195">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-195">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb8bd-196">b.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-196">b.</span></span> <span data-ttu-id="fb8bd-197">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-197">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fb8bd-198">c.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-198">c.</span></span> <span data-ttu-id="fb8bd-199">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-199">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fb8bd-200">d.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-200">d.</span></span> <span data-ttu-id="fb8bd-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="fb8bd-202">Creación de un usuario de prueba de YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="fb8bd-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="fb8bd-203">En esta sección, creará una usuaria llamada Britta Simon en YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="fb8bd-204">Trabaje con usuarios YouEarnedIt compatibilidad con team tooadd hello en la plataforma de YouEarnedIt Hola.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-204">Please work with YouEarnedIt support team tooadd hello users in hello YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="fb8bd-205">YouEarnedIt esperar Hola proveedor de identidades toosupply un EmailAddress o el nombre de usuario en el atributo de hello NameID.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-205">YouEarnedIt expect hello Identity Provider toosupply an EmailAddress  or UserName in hello NameID attribute.</span></span> <span data-ttu-id="fb8bd-206">Se producirá un error en la autenticación si un nombre de usuario correspondiente o EmailAddress no se encuentra en la base de datos de Hola o no coincide exactamente.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within hello database or does not match exactly.</span></span> <span data-ttu-id="fb8bd-207">Esto requerirá que se importan las cuentas de sistema de YouEarnedIt de hello antes de la integración de SSO de hello (normalmente ya sea a través de la importación de API o CSV).</span><span class="sxs-lookup"><span data-stu-id="fb8bd-207">This will require that accounts be imported into hello YouEarnedIt system before hello SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fb8bd-208">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb8bd-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fb8bd-209">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYouEarnedIt.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="fb8bd-211">**tooassign Britta Simon tooYouEarnedIt, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb8bd-211">**tooassign Britta Simon tooYouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb8bd-212">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fb8bd-214">En la lista de aplicaciones de hello, seleccione **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-214">In hello applications list, select **YouEarnedIt**.</span></span>

    ![vínculo de YouEarnedIt Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="fb8bd-216">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="fb8bd-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-218">Click **Add** button.</span></span> <span data-ttu-id="fb8bd-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="fb8bd-221">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb8bd-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb8bd-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fb8bd-224">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="fb8bd-224">Test single sign-on</span></span>

<span data-ttu-id="fb8bd-225">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fb8bd-226">Al hacer clic en icono de YouEarnedIt Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour YouEarnedIt aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb8bd-226">When you click hello YouEarnedIt tile in hello Access Panel, you should get automatically signed-on tooyour YouEarnedIt application.</span></span>
<span data-ttu-id="fb8bd-227">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fb8bd-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fb8bd-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fb8bd-228">Additional resources</span></span>

* [<span data-ttu-id="fb8bd-229">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb8bd-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb8bd-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb8bd-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

