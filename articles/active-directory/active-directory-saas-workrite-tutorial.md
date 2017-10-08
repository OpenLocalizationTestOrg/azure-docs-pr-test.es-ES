---
title: "Tutorial: Integración de Azure Active Directory con Workrite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a663374ae3c8b102b53d8cf05a9cb083b80dbb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="0bc36-103">Tutorial: Integración de Azure Active Directory con Workrite</span><span class="sxs-lookup"><span data-stu-id="0bc36-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="0bc36-104">En este tutorial, aprenderá cómo toointegrate Workrite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0bc36-104">In this tutorial, you learn how toointegrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0bc36-105">Integración Workrite con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0bc36-105">Integrating Workrite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0bc36-106">Puede controlar en Azure AD que tenga acceso tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="0bc36-106">You can control in Azure AD who has access tooWorkrite.</span></span>
- <span data-ttu-id="0bc36-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkrite (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bc36-107">You can enable your users tooautomatically get signed-on tooWorkrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0bc36-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bc36-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0bc36-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0bc36-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bc36-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0bc36-110">Prerequisites</span></span>

<span data-ttu-id="0bc36-111">integración de Azure AD con Workrite tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0bc36-111">tooconfigure Azure AD integration with Workrite, you need hello following items:</span></span>

- <span data-ttu-id="0bc36-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bc36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0bc36-113">Una suscripción habilitada para el inicio de sesión único en Workrite</span><span class="sxs-lookup"><span data-stu-id="0bc36-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0bc36-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0bc36-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0bc36-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0bc36-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0bc36-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0bc36-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0bc36-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bc36-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0bc36-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0bc36-118">Scenario description</span></span>
<span data-ttu-id="0bc36-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0bc36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0bc36-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0bc36-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0bc36-121">Agregar Workrite desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0bc36-121">Adding Workrite from hello gallery</span></span>
2. <span data-ttu-id="0bc36-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bc36-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-hello-gallery"></a><span data-ttu-id="0bc36-123">Agregar Workrite desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0bc36-123">Adding Workrite from hello gallery</span></span>
<span data-ttu-id="0bc36-124">integración de hello tooconfigure de Workrite en Azure AD, deberá tooadd Workrite de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0bc36-124">tooconfigure hello integration of Workrite into Azure AD, you need tooadd Workrite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0bc36-125">**tooadd Workrite de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bc36-125">**tooadd Workrite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bc36-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0bc36-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="0bc36-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0bc36-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="0bc36-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bc36-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="0bc36-133">En el cuadro de búsqueda de hello, escriba **Workrite**, seleccione **Workrite** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0bc36-133">In hello search box, type **Workrite**, select **Workrite** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workrite en la lista de resultados de Hola](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0bc36-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bc36-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0bc36-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Workrite con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0bc36-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0bc36-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Workrite es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bc36-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workrite is tooa user in Azure AD.</span></span> <span data-ttu-id="0bc36-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Workrite debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0bc36-138">In other words, a link relationship between an Azure AD user and hello related user in Workrite needs toobe established.</span></span>

<span data-ttu-id="0bc36-139">En Workrite, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bc36-139">In Workrite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0bc36-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Workrite, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0bc36-140">tooconfigure and test Azure AD single sign-on with Workrite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0bc36-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0bc36-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0bc36-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0bc36-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0bc36-143">**[Crear un usuario de prueba Workrite](#create-a-workrite-test-user)**  -toohave un equivalente de Britta Simon en Workrite que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0bc36-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - toohave a counterpart of Britta Simon in Workrite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0bc36-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0bc36-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0bc36-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0bc36-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0bc36-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bc36-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0bc36-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Workrite.</span><span class="sxs-lookup"><span data-stu-id="0bc36-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="0bc36-148">**inicio de sesión único en Azure AD tooconfigure con Workrite, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bc36-148">**tooconfigure Azure AD single sign-on with Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bc36-149">En el portal de Azure, en Hola Hola **Workrite** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-149">In hello Azure portal, on hello **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="0bc36-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0bc36-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="0bc36-153">En hello **Workrite dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0bc36-153">On hello **Workrite Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="0bc36-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="0bc36-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0bc36-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="0bc36-156">This value is not real.</span></span> <span data-ttu-id="0bc36-157">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="0bc36-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0bc36-158">Póngase en contacto con [equipo de soporte técnico de cliente de Workrite](mailto:support@workrite.co.uk) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="0bc36-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) tooget this value.</span></span>

4. <span data-ttu-id="0bc36-159">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0bc36-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="0bc36-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0bc36-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0bc36-163">En hello **Workrite configuración** sección, haga clic en **configurar Workrite** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0bc36-163">On hello **Workrite Configuration** section, click **Configure Workrite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0bc36-164">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0bc36-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="0bc36-166">inicio de sesión único en tooconfigure en **Workrite** lado, necesita hello toosend descargado **Certificate(Base64), dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado[Workrite equipo de soporte técnico](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="0bc36-166">tooconfigure single sign-on on **Workrite** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="0bc36-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0bc36-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0bc36-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0bc36-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0bc36-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0bc36-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0bc36-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bc36-170">Create an Azure AD test user</span></span>

<span data-ttu-id="0bc36-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0bc36-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="0bc36-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bc36-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bc36-174">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="0bc36-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0bc36-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0bc36-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bc36-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0bc36-180">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0bc36-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0bc36-182">a.</span><span class="sxs-lookup"><span data-stu-id="0bc36-182">a.</span></span> <span data-ttu-id="0bc36-183">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0bc36-184">b.</span><span class="sxs-lookup"><span data-stu-id="0bc36-184">b.</span></span> <span data-ttu-id="0bc36-185">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0bc36-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0bc36-186">c.</span><span class="sxs-lookup"><span data-stu-id="0bc36-186">c.</span></span> <span data-ttu-id="0bc36-187">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="0bc36-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0bc36-188">d.</span><span class="sxs-lookup"><span data-stu-id="0bc36-188">d.</span></span> <span data-ttu-id="0bc36-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="0bc36-190">Creación de un usuario de prueba de Workrite</span><span class="sxs-lookup"><span data-stu-id="0bc36-190">Create a Workrite test user</span></span>

<span data-ttu-id="0bc36-191">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Workrite toocreate.</span><span class="sxs-lookup"><span data-stu-id="0bc36-191">hello objective of this section is toocreate a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="0bc36-192">**toocreate un usuario llamado Britta Simon en Workrite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bc36-192">**toocreate a user called Britta Simon in Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bc36-193">Inicie sesión en el sitio de empresa de tooyour workrite como administrador.</span><span class="sxs-lookup"><span data-stu-id="0bc36-193">Sign on tooyour workrite company site as administrator.</span></span>

2. <span data-ttu-id="0bc36-194">En el panel de navegación de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-194">In hello navigation pane, click **Admin**.</span></span>
   
    ![Control de administración][400]

3. <span data-ttu-id="0bc36-196">Vaya tooQuick vínculos y, a continuación, haga clic en **crear un usuario**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-196">Go tooQuick Links, and then click **Create a User**.</span></span>
   
    ![Sección Crear usuario][401]

4. <span data-ttu-id="0bc36-198">En hello **Create User** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0bc36-198">On hello **Create User** dialog, perform hello following steps:</span></span>
   
    ![Cuadro de diálogo Crear usuario][402]
    
    <span data-ttu-id="0bc36-200">a.</span><span class="sxs-lookup"><span data-stu-id="0bc36-200">a.</span></span> <span data-ttu-id="0bc36-201">Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0bc36-201">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="0bc36-202">b.</span><span class="sxs-lookup"><span data-stu-id="0bc36-202">b.</span></span> <span data-ttu-id="0bc36-203">Hola **nombre** cuadro de texto, tipo hello firstname del usuario como Bárbara.</span><span class="sxs-lookup"><span data-stu-id="0bc36-203">In hello **First Name** textbox, type hello firstname of user like Britta.</span></span>

    <span data-ttu-id="0bc36-204">c.</span><span class="sxs-lookup"><span data-stu-id="0bc36-204">c.</span></span> <span data-ttu-id="0bc36-205">Hola **apellido** cuadro de texto, apellido de Hola de tipo de usuario como Simon.</span><span class="sxs-lookup"><span data-stu-id="0bc36-205">In hello **Surname** textbox, type hello surname of user like Simon.</span></span>
    
    <span data-ttu-id="0bc36-206">d.</span><span class="sxs-lookup"><span data-stu-id="0bc36-206">d.</span></span> <span data-ttu-id="0bc36-207">Seleccione **Administrador de cliente** como **Elegir rol**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="0bc36-208">e.</span><span class="sxs-lookup"><span data-stu-id="0bc36-208">e.</span></span> <span data-ttu-id="0bc36-209">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-209">Click **Save**.</span></span>   

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0bc36-210">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bc36-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0bc36-211">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="0bc36-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkrite.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="0bc36-213">**tooassign Britta Simon tooWorkrite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bc36-213">**tooassign Britta Simon tooWorkrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bc36-214">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0bc36-216">En la lista de aplicaciones de hello, seleccione **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-216">In hello applications list, select **Workrite**.</span></span>

    ![vínculo de Workrite Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="0bc36-218">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="0bc36-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-220">Click **Add** button.</span></span> <span data-ttu-id="0bc36-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="0bc36-223">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bc36-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0bc36-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0bc36-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0bc36-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0bc36-226">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0bc36-226">Test single sign-on</span></span>

<span data-ttu-id="0bc36-227">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0bc36-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0bc36-228">Al hacer clic en icono de Workrite Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Workrite aplicación.</span><span class="sxs-lookup"><span data-stu-id="0bc36-228">When you click hello Workrite tile in hello Access Panel, you should get automatically signed-on tooyour Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0bc36-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0bc36-229">Additional resources</span></span>

* [<span data-ttu-id="0bc36-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bc36-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0bc36-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0bc36-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

