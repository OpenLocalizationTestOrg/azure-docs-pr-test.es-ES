---
title: "Tutorial: Integración de Azure Active Directory con FileCloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="7b29e-103">Tutorial: integración de Azure Active Directory con FileCloud</span><span class="sxs-lookup"><span data-stu-id="7b29e-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="7b29e-104">En este tutorial, aprenderá cómo toointegrate FileCloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b29e-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b29e-105">Integración FileCloud con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7b29e-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b29e-106">Puede controlar en Azure AD que tenga acceso tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="7b29e-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="7b29e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFileCloud (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b29e-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7b29e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b29e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7b29e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b29e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b29e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b29e-110">Prerequisites</span></span>

<span data-ttu-id="7b29e-111">integración de Azure AD con FileCloud tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7b29e-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="7b29e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b29e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b29e-113">Una suscripción habilitada para el inicio de sesión único en FileCloud</span><span class="sxs-lookup"><span data-stu-id="7b29e-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b29e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7b29e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b29e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7b29e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b29e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7b29e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b29e-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b29e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b29e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7b29e-118">Scenario description</span></span>
<span data-ttu-id="7b29e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7b29e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b29e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7b29e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b29e-121">Agregar FileCloud desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7b29e-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="7b29e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b29e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="7b29e-123">Agregar FileCloud desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7b29e-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="7b29e-124">integración de hello tooconfigure de FileCloud en Azure AD, deberá tooadd FileCloud de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7b29e-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b29e-125">**tooadd FileCloud de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b29e-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b29e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7b29e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="7b29e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b29e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="7b29e-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b29e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="7b29e-133">En el cuadro de búsqueda de hello, escriba **FileCloud**, seleccione **FileCloud** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7b29e-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![FileCloud en la lista de resultados de Hola](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7b29e-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b29e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7b29e-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FileCloud con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7b29e-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b29e-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en FileCloud es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b29e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="7b29e-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en FileCloud debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7b29e-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="7b29e-139">En FileCloud, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b29e-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b29e-140">tooconfigure y prueba de inicio de sesión único en Azure AD con FileCloud, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7b29e-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b29e-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7b29e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b29e-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b29e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b29e-143">**[Crear un usuario de prueba FileCloud](#create-a-filecloud-test-user)**  -toohave un equivalente de Britta Simon en FileCloud que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="7b29e-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b29e-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7b29e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b29e-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7b29e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7b29e-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b29e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7b29e-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación FileCloud.</span><span class="sxs-lookup"><span data-stu-id="7b29e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="7b29e-148">**inicio de sesión único en Azure AD tooconfigure con FileCloud, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b29e-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b29e-149">En el portal de Azure, en Hola Hola **FileCloud** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="7b29e-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7b29e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="7b29e-153">En hello **FileCloud dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7b29e-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="7b29e-155">a.</span><span class="sxs-lookup"><span data-stu-id="7b29e-155">a.</span></span> <span data-ttu-id="7b29e-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="7b29e-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="7b29e-157">b.</span><span class="sxs-lookup"><span data-stu-id="7b29e-157">b.</span></span> <span data-ttu-id="7b29e-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="7b29e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b29e-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7b29e-159">These values are not real.</span></span> <span data-ttu-id="7b29e-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="7b29e-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7b29e-161">Póngase en contacto con [equipo de soporte técnico de cliente de FileCloud](mailto:support@codelathe.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="7b29e-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="7b29e-162">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7b29e-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="7b29e-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7b29e-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b29e-166">En hello **FileCloud configuración** sección, haga clic en **configurar FileCloud** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="7b29e-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b29e-167">Hola copia **Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="7b29e-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuración de FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="7b29e-169">En una ventana del explorador web diferente, inicio de sesión tooyour FileCloud inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="7b29e-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="7b29e-170">En el panel de navegación izquierdo de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![Sección Configuración en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="7b29e-172">Haga clic en la ficha **SSO** de la sección de configuración.</span><span class="sxs-lookup"><span data-stu-id="7b29e-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Pestaña Inicio de sesión único en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="7b29e-174">Seleccione **SAML** como **Default SSO Type** (Tipo de SSO predeterminado) en el panel **Configuración de inicio de sesión único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Panel de configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="7b29e-176">Pegar **Id. de entidad SAML**, que han copiado desde el portal de Azure en hello **dirección URL de extremo IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="7b29e-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![Cuadro de texto Dirección URL del punto de conexión del IDP](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="7b29e-178">Abra el archivo de metadatos descargado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **metadatos de IdP** en el cuadro de texto **configuración SAML** panel.</span><span class="sxs-lookup"><span data-stu-id="7b29e-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Sección de metadatos del IDP en la aplicación](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="7b29e-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7b29e-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="7b29e-181">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="7b29e-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b29e-182">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="7b29e-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b29e-183">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b29e-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7b29e-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b29e-184">Create an Azure AD test user</span></span>

<span data-ttu-id="7b29e-185">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7b29e-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="7b29e-187">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b29e-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b29e-188">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="7b29e-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7b29e-190">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7b29e-192">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b29e-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7b29e-194">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7b29e-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7b29e-196">a.</span><span class="sxs-lookup"><span data-stu-id="7b29e-196">a.</span></span> <span data-ttu-id="7b29e-197">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b29e-198">b.</span><span class="sxs-lookup"><span data-stu-id="7b29e-198">b.</span></span> <span data-ttu-id="7b29e-199">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b29e-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7b29e-200">c.</span><span class="sxs-lookup"><span data-stu-id="7b29e-200">c.</span></span> <span data-ttu-id="7b29e-201">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="7b29e-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7b29e-202">d.</span><span class="sxs-lookup"><span data-stu-id="7b29e-202">d.</span></span> <span data-ttu-id="7b29e-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="7b29e-204">Creación de un usuario de prueba de FileCloud</span><span class="sxs-lookup"><span data-stu-id="7b29e-204">Create a FileCloud test user</span></span>

<span data-ttu-id="7b29e-205">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en FileCloud toocreate.</span><span class="sxs-lookup"><span data-stu-id="7b29e-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="7b29e-206">FileCloud admite el aprovisionamiento just-in-time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7b29e-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7b29e-207">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="7b29e-207">There is no action item for you in this section.</span></span> <span data-ttu-id="7b29e-208">Se crea un nuevo usuario durante un tooaccess intento FileCloud si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="7b29e-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7b29e-209">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de FileCloud cliente](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="7b29e-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7b29e-210">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b29e-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7b29e-211">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="7b29e-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="7b29e-213">**tooassign Britta Simon tooFileCloud, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b29e-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b29e-214">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7b29e-216">En la lista de aplicaciones de hello, seleccione **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-216">In hello applications list, select **FileCloud**.</span></span>

    ![vínculo de FileCloud Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="7b29e-218">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="7b29e-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-220">Click **Add** button.</span></span> <span data-ttu-id="7b29e-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="7b29e-223">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b29e-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b29e-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b29e-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7b29e-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7b29e-226">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="7b29e-226">Test single sign-on</span></span>

<span data-ttu-id="7b29e-227">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7b29e-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b29e-228">Al hacer clic en icono de FileCloud Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour FileCloud aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b29e-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b29e-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7b29e-229">Additional resources</span></span>

* [<span data-ttu-id="7b29e-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b29e-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b29e-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b29e-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

