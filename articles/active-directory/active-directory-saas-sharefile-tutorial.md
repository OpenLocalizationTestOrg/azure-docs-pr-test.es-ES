---
title: "Tutorial: Integración de Azure Active Directory con Citrix ShareFile | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="6d3cd-103">Tutorial: Integración de Azure Active Directory con Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6d3cd-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="6d3cd-104">En este tutorial, aprenderá cómo toointegrate Citrix ShareFile con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d3cd-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d3cd-105">Integración de Citrix ShareFile con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6d3cd-106">Puede controlar en Azure AD que tenga acceso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="6d3cd-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCitrix ShareFile (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6d3cd-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6d3cd-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d3cd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d3cd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6d3cd-110">Prerequisites</span></span>

<span data-ttu-id="6d3cd-111">tooconfigure integración de Azure AD con Citrix ShareFile, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="6d3cd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d3cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d3cd-113">Una suscripción habilitada para el inicio de sesión único en Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6d3cd-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d3cd-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d3cd-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d3cd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d3cd-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d3cd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d3cd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6d3cd-118">Scenario description</span></span>
<span data-ttu-id="6d3cd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d3cd-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d3cd-121">Agregar Citrix ShareFile de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6d3cd-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="6d3cd-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d3cd-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="6d3cd-123">Agregar Citrix ShareFile de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6d3cd-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="6d3cd-124">integración de hello tooconfigure de Citrix ShareFile en Azure AD, deberá tooadd Citrix ShareFile de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6d3cd-125">**tooadd Citrix ShareFile desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d3cd-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d3cd-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="6d3cd-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6d3cd-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="6d3cd-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="6d3cd-133">En el cuadro de búsqueda de hello, escriba **Citrix ShareFile**, seleccione **Citrix ShareFile** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de Citrix ShareFile Hola](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6d3cd-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d3cd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6d3cd-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Citrix ShareFile con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6d3cd-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6d3cd-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Citrix ShareFile es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="6d3cd-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Citrix ShareFile debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="6d3cd-139">En Citrix ShareFile, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6d3cd-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Citrix ShareFile, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6d3cd-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6d3cd-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d3cd-143">**[Crear un usuario de prueba de Citrix ShareFile](#create-a-citrix-sharefile-test-user) ** -toohave un equivalente de Britta Simon en Citrix ShareFile que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d3cd-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d3cd-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6d3cd-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d3cd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6d3cd-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="6d3cd-148">**inicio de sesión único en tooconfigure Azure AD con Citrix ShareFile, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d3cd-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d3cd-149">En el portal de Azure, en Hola Hola **Citrix ShareFile** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="6d3cd-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="6d3cd-153">En hello **Citrix ShareFile dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="6d3cd-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="6d3cd-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d3cd-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-156">This value is not real.</span></span> <span data-ttu-id="6d3cd-157">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6d3cd-158">Póngase en contacto con [equipo de soporte técnico de Citrix ShareFile cliente](https://www.citrix.co.in/products/sharefile/support.html) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="6d3cd-159">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="6d3cd-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6d3cd-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6d3cd-163">En hello **configuración de Citrix ShareFile** sección, haga clic en **configurar Citrix ShareFile** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6d3cd-164">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="6d3cd-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="6d3cd-166">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de **Citrix ShareFile** .</span><span class="sxs-lookup"><span data-stu-id="6d3cd-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="6d3cd-167">En la barra de herramientas de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="6d3cd-168">En el panel de navegación izquierdo de hello, seleccione **configurar Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="6d3cd-169">![Administración de cuentas](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Administración de cuentas")</span><span class="sxs-lookup"><span data-stu-id="6d3cd-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="6d3cd-170">En hello **Single Sign-On / configuración de SAML 2.0** página de diálogo en **configuración básica**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="6d3cd-171">![Inicio de sesión único](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6d3cd-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="6d3cd-172">a.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-172">a.</span></span> <span data-ttu-id="6d3cd-173">Haga clic en **Enable SAML**(Habilitar SAML).</span><span class="sxs-lookup"><span data-stu-id="6d3cd-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="6d3cd-174">b.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-174">b.</span></span> <span data-ttu-id="6d3cd-175">En **su emisor de IDP / Id. de entidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6d3cd-176">c.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-176">c.</span></span> <span data-ttu-id="6d3cd-177">Haga clic en **cambio** toohello siguiente **certificado X.509** campo y, a continuación, cargar certificado de Hola que descargó desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="6d3cd-178">d.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-178">d.</span></span> <span data-ttu-id="6d3cd-179">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6d3cd-180">e.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-180">e.</span></span> <span data-ttu-id="6d3cd-181">En **Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="6d3cd-182">Haga clic en **guardar** en hello portal de administración de Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="6d3cd-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="6d3cd-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6d3cd-184">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6d3cd-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d3cd-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6d3cd-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d3cd-186">Create an Azure AD test user</span></span>

<span data-ttu-id="6d3cd-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="6d3cd-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d3cd-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d3cd-190">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6d3cd-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6d3cd-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6d3cd-196">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6d3cd-198">a.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-198">a.</span></span> <span data-ttu-id="6d3cd-199">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d3cd-200">b.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-200">b.</span></span> <span data-ttu-id="6d3cd-201">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6d3cd-202">c.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-202">c.</span></span> <span data-ttu-id="6d3cd-203">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6d3cd-204">d.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-204">d.</span></span> <span data-ttu-id="6d3cd-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="6d3cd-206">Creación de un usuario de prueba de Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6d3cd-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="6d3cd-207">En orden tooenable toolog de los usuarios de Azure AD en Citrix ShareFile, se les deben aprovisionar en Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="6d3cd-208">En caso de hello de Citrix ShareFile, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="6d3cd-209">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d3cd-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d3cd-210">Inicie sesión en tooyour **Citrix ShareFile** inquilino.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="6d3cd-211">Haga clic en **Manage Users \> (Administrar usuarios) Manage Users Home \> (Administrar página de inicio de usuarios) + Create Employee** (Crear empleado).</span><span class="sxs-lookup"><span data-stu-id="6d3cd-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="6d3cd-212">![Crear empleado](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Crear empleado")</span><span class="sxs-lookup"><span data-stu-id="6d3cd-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="6d3cd-213">En hello **información básica** sección, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6d3cd-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="6d3cd-214">![Información básica](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Información básica")</span><span class="sxs-lookup"><span data-stu-id="6d3cd-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="6d3cd-215">a.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-215">a.</span></span> <span data-ttu-id="6d3cd-216">Hola **dirección de correo electrónico** cuadro de texto, dirección de correo electrónico de tipo hello de Britta Simon como ** brittasimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="6d3cd-217">b.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-217">b.</span></span> <span data-ttu-id="6d3cd-218">Hola **nombre** cuadro de texto, tipo **nombre** del usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="6d3cd-219">c.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-219">c.</span></span> <span data-ttu-id="6d3cd-220">Hola **Last Name** cuadro de texto, tipo **apellidos** del usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="6d3cd-221">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="6d3cd-222">titular de la cuenta de Hello Azure AD recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla. Puede usar cualquier otra Citrix ShareFile usuario cuenta herramienta de creación o las API proporcionadas por Citrix ShareFile tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6d3cd-223">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d3cd-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6d3cd-224">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="6d3cd-226">**tooassign tooCitrix Britta Simon ShareFile, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d3cd-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d3cd-227">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6d3cd-229">En la lista de aplicaciones de hello, seleccione **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Hola Citrix ShareFile vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="6d3cd-231">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="6d3cd-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-233">Click **Add** button.</span></span> <span data-ttu-id="6d3cd-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="6d3cd-236">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6d3cd-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d3cd-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6d3cd-239">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="6d3cd-239">Test single sign-on</span></span>

<span data-ttu-id="6d3cd-240">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6d3cd-241">Al hacer clic en hello Citrix ShareFile disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6d3cd-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="6d3cd-242">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d3cd-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6d3cd-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d3cd-243">Additional resources</span></span>

* [<span data-ttu-id="6d3cd-244">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d3cd-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d3cd-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d3cd-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

