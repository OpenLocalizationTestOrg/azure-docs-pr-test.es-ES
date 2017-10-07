---
title: "Tutorial: integración de Azure Active Directory con ClickTime | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="c7a8b-103">Tutorial: integración de Azure Active Directory con ClickTime</span><span class="sxs-lookup"><span data-stu-id="c7a8b-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="c7a8b-104">En este tutorial, aprenderá cómo toointegrate ClickTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7a8b-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7a8b-105">Integración de ClickTime con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7a8b-106">Puede controlar en Azure AD que tenga acceso tooClickTime</span><span class="sxs-lookup"><span data-stu-id="c7a8b-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="c7a8b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooClickTime (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a8b-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7a8b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c7a8b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7a8b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7a8b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7a8b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c7a8b-110">Prerequisites</span></span>

<span data-ttu-id="c7a8b-111">integración de Azure AD con ClickTime tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="c7a8b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7a8b-113">Una suscripción habilitada para el inicio de sesión único en ClickTime</span><span class="sxs-lookup"><span data-stu-id="c7a8b-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7a8b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7a8b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7a8b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7a8b-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7a8b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7a8b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c7a8b-118">Scenario description</span></span>
<span data-ttu-id="c7a8b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7a8b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7a8b-121">Agregar ClickTime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c7a8b-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="c7a8b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="c7a8b-123">Agregar ClickTime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c7a8b-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="c7a8b-124">integración de hello tooconfigure de ClickTime en Azure AD, deberá tooadd ClickTime de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7a8b-125">**tooadd ClickTime de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c7a8b-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a8b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="c7a8b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7a8b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="c7a8b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="c7a8b-133">En el cuadro de búsqueda de hello, escriba **ClickTime**, seleccione **ClickTime** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de ClickTime Hola](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c7a8b-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a8b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c7a8b-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ClickTime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c7a8b-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7a8b-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ClickTime es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="c7a8b-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ClickTime debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="c7a8b-139">En ClickTime, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7a8b-140">tooconfigure y prueba de inicio de sesión único en Azure AD con ClickTime, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7a8b-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7a8b-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7a8b-143">**[Crear un usuario de prueba de ClickTime](#create-a-clicktime-test-user)**  -toohave un equivalente de Britta Simon en ClickTime que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7a8b-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7a8b-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c7a8b-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a8b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c7a8b-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de ClickTime.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="c7a8b-148">**inicio de sesión único en tooconfigure Azure AD con ClickTime, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c7a8b-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a8b-149">En el portal de Azure, en Hola Hola **ClickTime** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="c7a8b-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="c7a8b-153">En hello **ClickTime dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="c7a8b-155">a.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-155">a.</span></span> <span data-ttu-id="c7a8b-156">Hola **identificador** cuadro de texto, escriba una dirección URL como:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="c7a8b-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="c7a8b-157">b.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-157">b.</span></span> <span data-ttu-id="c7a8b-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="c7a8b-159">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="c7a8b-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c7a8b-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7a8b-163">En hello **configuración de ClickTime** sección, haga clic en **configurar ClickTime** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c7a8b-164">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c7a8b-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="c7a8b-166">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de ClickTime como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="c7a8b-167">En la barra de herramientas de hello en la parte superior de hello, haga clic en **preferencias**y, a continuación, haga clic en **configuración de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="c7a8b-168">Hola **preferencias de inicio de sesión único** configuración sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c7a8b-169">![Configuración de seguridad](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Configuración de seguridad")</span><span class="sxs-lookup"><span data-stu-id="c7a8b-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="c7a8b-170">a.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-170">a.</span></span>  <span data-ttu-id="c7a8b-171">Seleccione **Allow** sign-in using Single Sign-On (SSO) with **Azure AD** [Permitir inicio de sesión mediante inicio de sesión único (SSO) con Azure AD].</span><span class="sxs-lookup"><span data-stu-id="c7a8b-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="c7a8b-172">b.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-172">b.</span></span> <span data-ttu-id="c7a8b-173">Hola **extremo del proveedor de identidad** cuadro de texto, pegue **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c7a8b-174">c.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-174">c.</span></span>  <span data-ttu-id="c7a8b-175">Abra hello **certificado codificado en base 64** descargado desde el portal de Azure en **el Bloc de notas**, copiar el contenido de hello y, a continuación, péguelo en hello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="c7a8b-176">d.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-176">d.</span></span>  <span data-ttu-id="c7a8b-177">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c7a8b-178">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c7a8b-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7a8b-179">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7a8b-180">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7a8b-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c7a8b-181">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a8b-181">Create an Azure AD test user</span></span>
<span data-ttu-id="c7a8b-182">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="c7a8b-184">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c7a8b-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a8b-185">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7a8b-187">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7a8b-189">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7a8b-191">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7a8b-193">a.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-193">a.</span></span> <span data-ttu-id="c7a8b-194">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7a8b-195">b.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-195">b.</span></span> <span data-ttu-id="c7a8b-196">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7a8b-197">c.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-197">c.</span></span> <span data-ttu-id="c7a8b-198">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7a8b-199">d.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-199">d.</span></span> <span data-ttu-id="c7a8b-200">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="c7a8b-201">Creación de un usuario de prueba de ClickTime</span><span class="sxs-lookup"><span data-stu-id="c7a8b-201">Create a ClickTime test user</span></span>

<span data-ttu-id="c7a8b-202">En orden tooenable toolog de los usuarios de Azure AD en ClickTime, se les deben aprovisionar en ClickTime.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="c7a8b-203">En caso de hello de ClickTime, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="c7a8b-204">Puede usar cualquier otra ClickTime usuario cuenta herramienta de creación o las API proporcionadas por ClickTime tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="c7a8b-205">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c7a8b-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="c7a8b-206">Inicie sesión en tooyour **ClickTime** inquilino.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="c7a8b-207">En la barra de herramientas de hello en la parte superior de hello, haga clic en **empresa**y, a continuación, haga clic en **personas**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="c7a8b-208">![Personas](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="c7a8b-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="c7a8b-209">Haga clic en **Add Person**(Agregar persona).</span><span class="sxs-lookup"><span data-stu-id="c7a8b-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="c7a8b-210">![Agregar persona](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Agregar persona")</span><span class="sxs-lookup"><span data-stu-id="c7a8b-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="c7a8b-211">Hola sección nueva persona, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c7a8b-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c7a8b-212">![Personas](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="c7a8b-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="c7a8b-213">a.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-213">a.</span></span>  <span data-ttu-id="c7a8b-214">Hola **nombre completo** cuadro de texto, tipo de nombre completo del usuario como **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="c7a8b-215">b.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-215">b.</span></span>  <span data-ttu-id="c7a8b-216">Hola **dirección de correo electrónico** Hola de tipo de correo electrónico del usuario, cuadro de texto, como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c7a8b-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="c7a8b-217">Si desea, puede establecer propiedades adicionales del objeto de hello nueva persona.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="c7a8b-218">c.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-218">c.</span></span>  <span data-ttu-id="c7a8b-219">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c7a8b-220">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a8b-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c7a8b-221">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooClickTime.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="c7a8b-223">**tooassign Britta Simon tooClickTime, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c7a8b-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a8b-224">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c7a8b-226">En la lista de aplicaciones de hello, seleccione **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-226">In hello applications list, select **ClickTime**.</span></span>

    ![Vínculo de ClickTimne en la lista de aplicaciones de Hola](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="c7a8b-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="c7a8b-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-230">Click **Add** button.</span></span> <span data-ttu-id="c7a8b-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="c7a8b-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7a8b-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7a8b-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c7a8b-236">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="c7a8b-236">Test single sign-on</span></span>

<span data-ttu-id="c7a8b-237">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c7a8b-238">Al hacer clic en icono de ClickTime Hola Hola Panel de acceso, deberá obtener aplicaciones de ClickTime tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="c7a8b-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="c7a8b-239">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7a8b-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7a8b-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c7a8b-240">Additional resources</span></span>

* [<span data-ttu-id="c7a8b-241">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7a8b-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7a8b-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7a8b-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

