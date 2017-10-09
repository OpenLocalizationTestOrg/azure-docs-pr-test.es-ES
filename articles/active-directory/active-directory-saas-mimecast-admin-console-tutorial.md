---
title: "Tutorial: Integración de Azure Active Directory con Mimecast Admin Console | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la consola de administración de Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="27bff-103">Tutorial: Integración de Azure Active Directory con Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="27bff-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="27bff-104">En este tutorial, aprenderá cómo la consola de administración de Mimecast toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27bff-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27bff-105">Integración de la consola de administración de Mimecast con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="27bff-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27bff-106">Puede controlar en Azure AD que tenga acceso tooMimecast consola de administración.</span><span class="sxs-lookup"><span data-stu-id="27bff-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="27bff-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMimecast consola de administración (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27bff-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="27bff-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="27bff-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="27bff-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27bff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27bff-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="27bff-110">Prerequisites</span></span>

<span data-ttu-id="27bff-111">integración de Azure AD con la consola de administración de Mimecast tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="27bff-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="27bff-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27bff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27bff-113">Un suscripción habilitada para inicio de sesión único en Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="27bff-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27bff-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="27bff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27bff-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="27bff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27bff-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="27bff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27bff-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27bff-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27bff-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="27bff-118">Scenario description</span></span>
<span data-ttu-id="27bff-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="27bff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27bff-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="27bff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27bff-121">Agregar la consola de administración de Mimecast de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27bff-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="27bff-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27bff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="27bff-123">Agregar la consola de administración de Mimecast de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27bff-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="27bff-124">integración de hello tooconfigure de consola de administración de Mimecast en Azure AD, deberá tooadd consola de administración de Mimecast de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="27bff-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27bff-125">**tooadd consola de administración de Mimecast de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27bff-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27bff-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="27bff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="27bff-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="27bff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27bff-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27bff-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="27bff-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27bff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="27bff-133">En el cuadro de búsqueda de hello, escriba **consola de administración de Mimecast**, seleccione **consola de administración de Mimecast** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27bff-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de la consola de administración de Mimecast Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="27bff-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="27bff-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="27bff-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mimecast Admin Console con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="27bff-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27bff-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en la consola de administración de Mimecast es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27bff-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="27bff-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en la consola de administración de Mimecast debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="27bff-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="27bff-139">En la consola de administración de Mimecast, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="27bff-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27bff-140">tooconfigure y prueba de inicio de sesión único en Azure AD con la consola de administración de Mimecast, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="27bff-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27bff-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="27bff-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27bff-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27bff-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27bff-143">**[Crear un usuario de prueba de la consola de administración de Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave un equivalente de Britta Simon en la consola de administración de Mimecast es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="27bff-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27bff-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27bff-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27bff-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="27bff-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="27bff-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27bff-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="27bff-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de consola de administración de Mimecast.</span><span class="sxs-lookup"><span data-stu-id="27bff-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="27bff-148">**tooconfigure inicio de sesión único en Azure AD con la consola de administración de Mimecast, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27bff-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="27bff-149">En el portal de Azure, en Hola Hola **consola de administración de Mimecast** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="27bff-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="27bff-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27bff-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="27bff-153">En hello **Mimecast dominio de la consola de administración y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27bff-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="27bff-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:</span><span class="sxs-lookup"><span data-stu-id="27bff-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="27bff-156">dirección URL de inicio de sesión Hello es específica de la región.</span><span class="sxs-lookup"><span data-stu-id="27bff-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="27bff-157">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="27bff-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="27bff-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="27bff-159">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27bff-161">En hello **configuración de consola de administración de Mimecast** sección, haga clic en **configurar la consola de administración de Mimecast** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="27bff-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27bff-162">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="27bff-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="27bff-164">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="27bff-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="27bff-165">Vaya demasiado**servicios \> aplicación**.</span><span class="sxs-lookup"><span data-stu-id="27bff-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="27bff-166">![Servicios](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Servicios")</span><span class="sxs-lookup"><span data-stu-id="27bff-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="27bff-167">Haga clic en **Authentication Profiles**(Perfiles de autenticación).</span><span class="sxs-lookup"><span data-stu-id="27bff-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="27bff-168">![Authentication Profiles (Perfiles de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles (Perfiles de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="27bff-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="27bff-169">Haga clic en **New Authentication Profile**(Nuevo perfil de autenticación).</span><span class="sxs-lookup"><span data-stu-id="27bff-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="27bff-170">![New Authentication Profiles (Nuevos perfiles de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Authentication Profiles (Nuevos perfiles de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="27bff-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="27bff-171">Hola **perfil de autenticación** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27bff-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="27bff-172">![Authentication Profile (Perfil de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile (Perfil de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="27bff-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="27bff-173">a.</span><span class="sxs-lookup"><span data-stu-id="27bff-173">a.</span></span> <span data-ttu-id="27bff-174">Hola **descripción** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="27bff-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="27bff-175">b.</span><span class="sxs-lookup"><span data-stu-id="27bff-175">b.</span></span> <span data-ttu-id="27bff-176">Seleccione **Enforce SAML Authentication for Mimecast Admin Console**(Aplicar la autenticación SAML a Mimecast Admin Console).</span><span class="sxs-lookup"><span data-stu-id="27bff-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="27bff-177">c.</span><span class="sxs-lookup"><span data-stu-id="27bff-177">c.</span></span> <span data-ttu-id="27bff-178">Como **Provider** (Proveedor), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="27bff-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="27bff-179">d.</span><span class="sxs-lookup"><span data-stu-id="27bff-179">d.</span></span> <span data-ttu-id="27bff-180">Pegar **Id. de entidad SAML**, que haya copiado desde Hola portal de Azure en hello **dirección URL del emisor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="27bff-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="27bff-181">e.</span><span class="sxs-lookup"><span data-stu-id="27bff-181">e.</span></span> <span data-ttu-id="27bff-182">Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **dirección URL de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="27bff-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="27bff-183">f.</span><span class="sxs-lookup"><span data-stu-id="27bff-183">f.</span></span> <span data-ttu-id="27bff-184">Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **Logout URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="27bff-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="27bff-185">Hello valor de dirección URL de inicio de sesión y el valor de dirección URL de cierre de sesión de hello son para hello consola de administración de Mimecast Hola igual.</span><span class="sxs-lookup"><span data-stu-id="27bff-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="27bff-186">g.</span><span class="sxs-lookup"><span data-stu-id="27bff-186">g.</span></span> <span data-ttu-id="27bff-187">Abrir el certificado en base 64 se descarga desde el portal de Azure en el Bloc de notas, quitar la primera línea de hello ("*--*") y la última línea de hello ("*--*"), Hola copia restantes contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidades (metadatos)** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="27bff-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="27bff-188">h.</span><span class="sxs-lookup"><span data-stu-id="27bff-188">h.</span></span> <span data-ttu-id="27bff-189">Seleccione **Permitir inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="27bff-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="27bff-190">i.</span><span class="sxs-lookup"><span data-stu-id="27bff-190">i.</span></span> <span data-ttu-id="27bff-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="27bff-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="27bff-192">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="27bff-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27bff-193">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="27bff-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27bff-194">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27bff-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="27bff-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27bff-195">Create an Azure AD test user</span></span>

<span data-ttu-id="27bff-196">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="27bff-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="27bff-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27bff-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27bff-199">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="27bff-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="27bff-201">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="27bff-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="27bff-203">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27bff-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="27bff-205">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27bff-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="27bff-207">a.</span><span class="sxs-lookup"><span data-stu-id="27bff-207">a.</span></span> <span data-ttu-id="27bff-208">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27bff-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27bff-209">b.</span><span class="sxs-lookup"><span data-stu-id="27bff-209">b.</span></span> <span data-ttu-id="27bff-210">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27bff-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="27bff-211">c.</span><span class="sxs-lookup"><span data-stu-id="27bff-211">c.</span></span> <span data-ttu-id="27bff-212">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="27bff-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="27bff-213">d.</span><span class="sxs-lookup"><span data-stu-id="27bff-213">d.</span></span> <span data-ttu-id="27bff-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="27bff-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="27bff-215">Creación de un usuario de prueba de Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="27bff-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="27bff-216">En orden tooenable toolog de los usuarios de Azure AD en la consola de administración de Mimecast, se les deben aprovisionar en la consola de administración de Mimecast.</span><span class="sxs-lookup"><span data-stu-id="27bff-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="27bff-217">En caso de hello de la consola de administración de Mimecast, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="27bff-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="27bff-218">Deberá tooregister un dominio para poder crear los usuarios.</span><span class="sxs-lookup"><span data-stu-id="27bff-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="27bff-219">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27bff-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="27bff-220">Inicio de sesión tooyour **consola de administración de Mimecast** como administrador.</span><span class="sxs-lookup"><span data-stu-id="27bff-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="27bff-221">Vaya demasiado**directorios \> interno**.</span><span class="sxs-lookup"><span data-stu-id="27bff-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="27bff-222">![Directories (Directorios)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories (Directorios)")</span><span class="sxs-lookup"><span data-stu-id="27bff-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="27bff-223">Haga clic en **Register New Domain**(Registrar nuevo dominio).</span><span class="sxs-lookup"><span data-stu-id="27bff-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="27bff-224">![Register New Domain (Registrar nuevo dominio)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain (Registrar nuevo dominio)")</span><span class="sxs-lookup"><span data-stu-id="27bff-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="27bff-225">Una vez creado el nuevo dominio, haga clic en **New Address**(Nueva dirección).</span><span class="sxs-lookup"><span data-stu-id="27bff-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="27bff-226">![New Address (Nueva dirección)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address (Nueva dirección)")</span><span class="sxs-lookup"><span data-stu-id="27bff-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="27bff-227">Hola dirección cuadro de diálogo nuevo, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27bff-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="27bff-228">![Guardar](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Guardar")</span><span class="sxs-lookup"><span data-stu-id="27bff-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="27bff-229">a.</span><span class="sxs-lookup"><span data-stu-id="27bff-229">a.</span></span> <span data-ttu-id="27bff-230">Hola de tipo **dirección de correo electrónico**, **nombre Global**, **contraseña**, y **Confirmar contraseña** atributos de un anuncio de Azure válido de la cuenta desea tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="27bff-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="27bff-231">b.</span><span class="sxs-lookup"><span data-stu-id="27bff-231">b.</span></span> <span data-ttu-id="27bff-232">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="27bff-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="27bff-233">Puede usar cualquier otra herramienta de creación de cuentas de usuario de consola de administración de Mimecast o las API proporcionadas por las cuentas de usuario de consola de administración de Mimecast tooprovision Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27bff-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="27bff-234">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="27bff-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="27bff-235">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMimecast consola de administración.</span><span class="sxs-lookup"><span data-stu-id="27bff-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="27bff-237">**tooassign Britta Simon tooMimecast consola de administración, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27bff-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="27bff-238">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27bff-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="27bff-240">En la lista de aplicaciones de hello, seleccione **consola de administración de Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="27bff-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![vínculo de la consola de administración de Mimecast de Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="27bff-242">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27bff-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="27bff-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="27bff-244">Click **Add** button.</span></span> <span data-ttu-id="27bff-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27bff-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="27bff-247">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="27bff-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27bff-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27bff-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27bff-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27bff-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="27bff-250">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="27bff-250">Test single sign-on</span></span>

<span data-ttu-id="27bff-251">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="27bff-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="27bff-252">Al hacer clic en icono de la consola de administración de Mimecast de Hola Hola Panel de acceso, deberá obtener la aplicación de consola de administración de Mimecast tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="27bff-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="27bff-253">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="27bff-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27bff-254">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="27bff-254">Additional resources</span></span>

* [<span data-ttu-id="27bff-255">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27bff-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27bff-256">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27bff-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

