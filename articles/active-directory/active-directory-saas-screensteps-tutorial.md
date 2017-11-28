---
title: "Tutorial: Integración de Azure Active Directory con ScreenSteps | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="a84c4-103">Tutorial: Integración de Azure Active Directory con ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="a84c4-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="a84c4-104">En este tutorial, aprenderá cómo toointegrate ScreenSteps con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a84c4-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a84c4-105">Integración ScreenSteps con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a84c4-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a84c4-106">Puede controlar en Azure AD que tenga acceso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="a84c4-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="a84c4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooScreenSteps (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a84c4-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a84c4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a84c4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a84c4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a84c4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a84c4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a84c4-110">Prerequisites</span></span>

<span data-ttu-id="a84c4-111">integración de Azure AD con ScreenSteps tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a84c4-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="a84c4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a84c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a84c4-113">Una suscripción habilitada para el inicio de sesión único en ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="a84c4-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a84c4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a84c4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a84c4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a84c4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a84c4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a84c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a84c4-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a84c4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a84c4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a84c4-118">Scenario description</span></span>
<span data-ttu-id="a84c4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a84c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a84c4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="a84c4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a84c4-121">Agregar ScreenSteps desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a84c4-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="a84c4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a84c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="a84c4-123">Agregar ScreenSteps desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a84c4-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="a84c4-124">integración de hello tooconfigure de ScreenSteps en Azure AD, deberá tooadd ScreenSteps de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a84c4-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a84c4-125">**tooadd ScreenSteps de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a84c4-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a84c4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a84c4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="a84c4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a84c4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="a84c4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a84c4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="a84c4-133">En el cuadro de búsqueda de hello, escriba **ScreenSteps**, seleccione **ScreenSteps** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a84c4-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de ScreenSteps Hola](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a84c4-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="a84c4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a84c4-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ScreenSteps con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a84c4-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a84c4-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ScreenSteps es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a84c4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="a84c4-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ScreenSteps debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="a84c4-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="a84c4-139">En ScreenSteps, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a84c4-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a84c4-140">tooconfigure y prueba de inicio de sesión único en Azure AD con ScreenSteps, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a84c4-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a84c4-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="a84c4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a84c4-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a84c4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a84c4-143">**[Crear un usuario de prueba de ScreenSteps](#create-a-screensteps-test-user)**  -toohave un equivalente de Britta Simon en ScreenSteps que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="a84c4-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a84c4-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a84c4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a84c4-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a84c4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a84c4-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a84c4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a84c4-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="a84c4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="a84c4-148">**inicio de sesión único en tooconfigure Azure AD con ScreenSteps, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a84c4-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="a84c4-149">En el portal de Azure, en Hola Hola **ScreenSteps** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="a84c4-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a84c4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="a84c4-153">En hello **ScreenSteps dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a84c4-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="a84c4-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="a84c4-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a84c4-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="a84c4-156">This value is not real.</span></span> <span data-ttu-id="a84c4-157">Actualice este valor con hello Sign On URL real, que se explica más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a84c4-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="a84c4-158">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a84c4-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="a84c4-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a84c4-160">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a84c4-162">En hello **configuración de ScreenSteps** sección, haga clic en **configurar ScreenSteps** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="a84c4-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a84c4-163">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="a84c4-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="a84c4-165">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de ScreenSteps como administrador.</span><span class="sxs-lookup"><span data-stu-id="a84c4-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="a84c4-166">Haga clic en **Configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="a84c4-167">![Administración de cuentas](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Administración de cuentas")</span><span class="sxs-lookup"><span data-stu-id="a84c4-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="a84c4-168">Haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="a84c4-169">![Autenticación remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Autenticación remota")</span><span class="sxs-lookup"><span data-stu-id="a84c4-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="a84c4-170">Haga clic en **Crear punto de conexión de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="a84c4-171">![Autenticación remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Autenticación remota")</span><span class="sxs-lookup"><span data-stu-id="a84c4-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="a84c4-172">Hola **extremo de inicio de sesión único crear** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a84c4-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="a84c4-173">![Creación de un punto de conexión de autenticación](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Creación de un punto de conexión de autenticación")</span><span class="sxs-lookup"><span data-stu-id="a84c4-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="a84c4-174">a.</span><span class="sxs-lookup"><span data-stu-id="a84c4-174">a.</span></span> <span data-ttu-id="a84c4-175">Hola **título** cuadro de texto, escriba un título.</span><span class="sxs-lookup"><span data-stu-id="a84c4-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="a84c4-176">b.</span><span class="sxs-lookup"><span data-stu-id="a84c4-176">b.</span></span> <span data-ttu-id="a84c4-177">De hello **modo** lista, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="a84c4-178">c.</span><span class="sxs-lookup"><span data-stu-id="a84c4-178">c.</span></span> <span data-ttu-id="a84c4-179">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-179">Click **Create**.</span></span>

12. <span data-ttu-id="a84c4-180">**Editar** Hola nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="a84c4-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="a84c4-181">![Editar punto de conexión](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Editar punto de conexión")</span><span class="sxs-lookup"><span data-stu-id="a84c4-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="a84c4-182">Hola **extremo de inicio de sesión único editar** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a84c4-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="a84c4-183">![Punto de conexión de autenticación remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Punto de conexión de autenticación remota")</span><span class="sxs-lookup"><span data-stu-id="a84c4-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="a84c4-184">a.</span><span class="sxs-lookup"><span data-stu-id="a84c4-184">a.</span></span> <span data-ttu-id="a84c4-185">Haga clic en **carga de nuevo el archivo de certificado SAML**y, a continuación, carga Hola certificado en el que ha descargado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a84c4-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="a84c4-186">b.</span><span class="sxs-lookup"><span data-stu-id="a84c4-186">b.</span></span> <span data-ttu-id="a84c4-187">Pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **dirección URL de inicio de sesión remoto** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="a84c4-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="a84c4-188">c.</span><span class="sxs-lookup"><span data-stu-id="a84c4-188">c.</span></span> <span data-ttu-id="a84c4-189">Pegar **dirección URL de cierre de sesión** valor, que haya copiado desde Hola portal de Azure en hello **Log out URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="a84c4-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="a84c4-190">d.</span><span class="sxs-lookup"><span data-stu-id="a84c4-190">d.</span></span> <span data-ttu-id="a84c4-191">Seleccione un **grupo** tooassign toowhen de los usuarios que los haya aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="a84c4-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="a84c4-192">e.</span><span class="sxs-lookup"><span data-stu-id="a84c4-192">e.</span></span> <span data-ttu-id="a84c4-193">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="a84c4-193">Click **Update**.</span></span>

    <span data-ttu-id="a84c4-194">f.</span><span class="sxs-lookup"><span data-stu-id="a84c4-194">f.</span></span> <span data-ttu-id="a84c4-195">Hola copia **dirección URL del consumidor SAML** toohello Portapapeles y pegar en toohello **dirección URL de inicio de sesión** en el cuadro de texto **ScreenSteps dominio y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="a84c4-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="a84c4-196">g.</span><span class="sxs-lookup"><span data-stu-id="a84c4-196">g.</span></span> <span data-ttu-id="a84c4-197">Devolver toohello **extremo de inicio de sesión único editar**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="a84c4-198">h.</span><span class="sxs-lookup"><span data-stu-id="a84c4-198">h.</span></span> <span data-ttu-id="a84c4-199">Haga clic en hello **Predeterminar para cuenta** botón toouse este punto de conexión para todos los usuarios que inician sesión en ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="a84c4-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="a84c4-200">Como alternativa, puede hacer clic en hello **agregar tooSite** botón toouse este punto de conexión para sitios específicos de **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="a84c4-201">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="a84c4-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a84c4-202">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="a84c4-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a84c4-203">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a84c4-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a84c4-204">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a84c4-204">Create an Azure AD test user</span></span>

<span data-ttu-id="a84c4-205">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="a84c4-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="a84c4-207">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a84c4-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a84c4-208">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="a84c4-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a84c4-210">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a84c4-212">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a84c4-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a84c4-214">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a84c4-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a84c4-216">a.</span><span class="sxs-lookup"><span data-stu-id="a84c4-216">a.</span></span> <span data-ttu-id="a84c4-217">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a84c4-218">b.</span><span class="sxs-lookup"><span data-stu-id="a84c4-218">b.</span></span> <span data-ttu-id="a84c4-219">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a84c4-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a84c4-220">c.</span><span class="sxs-lookup"><span data-stu-id="a84c4-220">c.</span></span> <span data-ttu-id="a84c4-221">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="a84c4-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a84c4-222">d.</span><span class="sxs-lookup"><span data-stu-id="a84c4-222">d.</span></span> <span data-ttu-id="a84c4-223">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="a84c4-224">Creación de un usuario de prueba de ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="a84c4-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="a84c4-225">En esta sección, creará un usuario llamado Britta Simon en ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="a84c4-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="a84c4-226">Trabajar con [equipo de soporte técnico de ScreenSteps cliente](https://www.screensteps.com/contact) para agregar usuarios de hello en la plataforma de ScreenSteps Hola.</span><span class="sxs-lookup"><span data-stu-id="a84c4-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="a84c4-227">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a84c4-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a84c4-228">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a84c4-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a84c4-229">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="a84c4-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="a84c4-231">**tooassign Britta Simon tooScreenSteps, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a84c4-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="a84c4-232">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a84c4-234">En la lista de aplicaciones de hello, seleccione **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![vínculo de ScreenSteps Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="a84c4-236">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="a84c4-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-238">Click **Add** button.</span></span> <span data-ttu-id="a84c4-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="a84c4-241">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="a84c4-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a84c4-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a84c4-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a84c4-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a84c4-244">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a84c4-244">Test single sign-on</span></span>

<span data-ttu-id="a84c4-245">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a84c4-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a84c4-246">Al hacer clic en hello ScreenSteps disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour ScreenSteps aplicación.</span><span class="sxs-lookup"><span data-stu-id="a84c4-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="a84c4-247">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a84c4-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a84c4-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a84c4-248">Additional resources</span></span>

* [<span data-ttu-id="a84c4-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a84c4-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a84c4-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a84c4-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

