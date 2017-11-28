---
title: "Tutorial: Integración de Azure Active Directory con Sansan | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Sansan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: f58cc613a2e3a240e555b61a34db4155eb9dff71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="971e9-103">Tutorial: Integración de Azure Active Directory con Sansan</span><span class="sxs-lookup"><span data-stu-id="971e9-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="971e9-104">En este tutorial, aprenderá cómo toointegrate Sansan con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="971e9-104">In this tutorial, you learn how toointegrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="971e9-105">Integración Sansan con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="971e9-105">Integrating Sansan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="971e9-106">Puede controlar en Azure AD que tenga acceso tooSansan</span><span class="sxs-lookup"><span data-stu-id="971e9-106">You can control in Azure AD who has access tooSansan</span></span>
- <span data-ttu-id="971e9-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSansan (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="971e9-107">You can enable your users tooautomatically get signed-on tooSansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="971e9-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="971e9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="971e9-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="971e9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="971e9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="971e9-110">Prerequisites</span></span>

<span data-ttu-id="971e9-111">integración de Azure AD con Sansan tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="971e9-111">tooconfigure Azure AD integration with Sansan, you need hello following items:</span></span>

- <span data-ttu-id="971e9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="971e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="971e9-113">Una suscripción habilitada para el inicio de sesión único en Sansan</span><span class="sxs-lookup"><span data-stu-id="971e9-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="971e9-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="971e9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="971e9-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="971e9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="971e9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="971e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="971e9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="971e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="971e9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="971e9-118">Scenario description</span></span>
<span data-ttu-id="971e9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="971e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="971e9-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="971e9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="971e9-121">Agregar Sansan desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="971e9-121">Adding Sansan from hello gallery</span></span>
2. <span data-ttu-id="971e9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="971e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-hello-gallery"></a><span data-ttu-id="971e9-123">Agregar Sansan desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="971e9-123">Adding Sansan from hello gallery</span></span>
<span data-ttu-id="971e9-124">integración de hello tooconfigure de Sansan en Azure AD, deberá tooadd Sansan de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="971e9-124">tooconfigure hello integration of Sansan into Azure AD, you need tooadd Sansan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="971e9-125">**tooadd Sansan de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="971e9-125">**tooadd Sansan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="971e9-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="971e9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="971e9-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="971e9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="971e9-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="971e9-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="971e9-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="971e9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="971e9-133">En el cuadro de búsqueda de hello, escriba **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="971e9-133">In hello search box, type **Sansan**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="971e9-135">En el panel de resultados de hello, seleccione **Sansan**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="971e9-135">In hello results panel, select **Sansan**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="971e9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="971e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="971e9-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sansan con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="971e9-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="971e9-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Sansan es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="971e9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sansan is tooa user in Azure AD.</span></span> <span data-ttu-id="971e9-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Sansan debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="971e9-140">In other words, a link relationship between an Azure AD user and hello related user in Sansan needs toobe established.</span></span>

<span data-ttu-id="971e9-141">En Sansan, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="971e9-141">In Sansan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="971e9-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Sansan, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="971e9-142">tooconfigure and test Azure AD single sign-on with Sansan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="971e9-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="971e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="971e9-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="971e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="971e9-145">**[Crear un usuario de prueba Sansan](#creating-a-sansan-test-user) ** -toohave un equivalente de Britta Simon en Sansan que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="971e9-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - toohave a counterpart of Britta Simon in Sansan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="971e9-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="971e9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="971e9-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="971e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="971e9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="971e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="971e9-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Sansan.</span><span class="sxs-lookup"><span data-stu-id="971e9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="971e9-150">**inicio de sesión único en Azure AD tooconfigure con Sansan, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="971e9-150">**tooconfigure Azure AD single sign-on with Sansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="971e9-151">En el portal de Azure, en Hola Hola **Sansan** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="971e9-151">In hello Azure portal, on hello **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="971e9-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="971e9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="971e9-155">En hello **Sansan dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="971e9-155">On hello **Sansan Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="971e9-157">a.</span><span class="sxs-lookup"><span data-stu-id="971e9-157">a.</span></span> <span data-ttu-id="971e9-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="971e9-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | <span data-ttu-id="971e9-159">Environment</span><span class="sxs-lookup"><span data-stu-id="971e9-159">Environment</span></span> | <span data-ttu-id="971e9-160">URL</span><span class="sxs-lookup"><span data-stu-id="971e9-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="971e9-161">Web de PC</span><span class="sxs-lookup"><span data-stu-id="971e9-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="971e9-162">Aplicación nativa móvil</span><span class="sxs-lookup"><span data-stu-id="971e9-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="971e9-163">Configuración del explorador móvil</span><span class="sxs-lookup"><span data-stu-id="971e9-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="971e9-164">b.</span><span class="sxs-lookup"><span data-stu-id="971e9-164">b.</span></span> <span data-ttu-id="971e9-165">Hola **identificador** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="971e9-165">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="971e9-166">Environment</span><span class="sxs-lookup"><span data-stu-id="971e9-166">Environment</span></span>             | <span data-ttu-id="971e9-167">URL</span><span class="sxs-lookup"><span data-stu-id="971e9-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="971e9-168">Web de PC</span><span class="sxs-lookup"><span data-stu-id="971e9-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="971e9-169">Aplicación nativa móvil</span><span class="sxs-lookup"><span data-stu-id="971e9-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="971e9-170">Configuración del explorador móvil</span><span class="sxs-lookup"><span data-stu-id="971e9-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="971e9-171">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="971e9-171">These values are not real.</span></span> <span data-ttu-id="971e9-172">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="971e9-172">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="971e9-173">Póngase en contacto con [equipo de soporte técnico de cliente de Sansan](https://www.sansan.com/form/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="971e9-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) tooget these values.</span></span> 

4. <span data-ttu-id="971e9-174">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="971e9-174">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="971e9-176">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="971e9-176">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="971e9-178">En hello **Sansan configuración** sección, haga clic en **configurar Sansan** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="971e9-178">On hello **Sansan Configuration** section, click **Configure Sansan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="971e9-179">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="971e9-179">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="971e9-181">tooconfigure inicio de sesión único en **Sansan** lado, necesita hello toosend descargado **certificado**, **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML Single Sign-On dirección URL del servicio** demasiado[equipo de soporte técnico de Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="971e9-181">tooconfigure single sign-on on **Sansan** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="971e9-182">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="971e9-182">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="971e9-183">La configuración del explorador de PC también funciona para aplicaciones y exploradores móviles junto con la web del PC.</span><span class="sxs-lookup"><span data-stu-id="971e9-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="971e9-184">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="971e9-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="971e9-185">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="971e9-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="971e9-186">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="971e9-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="971e9-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="971e9-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="971e9-188">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="971e9-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="971e9-190">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="971e9-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="971e9-191">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="971e9-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="971e9-193">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="971e9-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="971e9-195">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="971e9-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="971e9-197">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="971e9-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="971e9-199">a.</span><span class="sxs-lookup"><span data-stu-id="971e9-199">a.</span></span> <span data-ttu-id="971e9-200">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="971e9-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="971e9-201">b.</span><span class="sxs-lookup"><span data-stu-id="971e9-201">b.</span></span> <span data-ttu-id="971e9-202">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="971e9-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="971e9-203">c.</span><span class="sxs-lookup"><span data-stu-id="971e9-203">c.</span></span> <span data-ttu-id="971e9-204">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="971e9-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="971e9-205">d.</span><span class="sxs-lookup"><span data-stu-id="971e9-205">d.</span></span> <span data-ttu-id="971e9-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="971e9-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="971e9-207">Creación de un usuario de prueba de Sansan</span><span class="sxs-lookup"><span data-stu-id="971e9-207">Creating a Sansan test user</span></span>

<span data-ttu-id="971e9-208">En esta sección, creará un usuario llamado Britta Simon en SanSan.</span><span class="sxs-lookup"><span data-stu-id="971e9-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="971e9-209">Aplicación de SanSan necesita hello toobe de usuario aprovisionado en aplicación hello antes de realizar SSO.</span><span class="sxs-lookup"><span data-stu-id="971e9-209">SanSan application needs hello user toobe provisioned in hello application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="971e9-210">Si necesita un usuario toocreate manualmente o por lotes de los usuarios, es necesario hello toocontact [equipo de soporte técnico de Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="971e9-210">If you need toocreate a user manually or batch of users, you need toocontact hello [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="971e9-211">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="971e9-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="971e9-212">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSansan.</span><span class="sxs-lookup"><span data-stu-id="971e9-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSansan.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="971e9-214">**tooassign Britta Simon tooSansan, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="971e9-214">**tooassign Britta Simon tooSansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="971e9-215">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="971e9-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="971e9-217">En la lista de aplicaciones de hello, seleccione **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="971e9-217">In hello applications list, select **Sansan**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="971e9-219">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="971e9-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="971e9-221">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="971e9-221">Click **Add** button.</span></span> <span data-ttu-id="971e9-222">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="971e9-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="971e9-224">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="971e9-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="971e9-225">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="971e9-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="971e9-226">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="971e9-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="971e9-227">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="971e9-227">Testing single sign-on</span></span>

<span data-ttu-id="971e9-228">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="971e9-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="971e9-229">Al hacer clic en icono de Sansan Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Sansan aplicación.</span><span class="sxs-lookup"><span data-stu-id="971e9-229">When you click hello Sansan tile in hello Access Panel, you should get automatically signed-on tooyour Sansan application.</span></span>
<span data-ttu-id="971e9-230">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="971e9-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="971e9-231">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="971e9-231">Additional resources</span></span>

* [<span data-ttu-id="971e9-232">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="971e9-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="971e9-233">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="971e9-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

