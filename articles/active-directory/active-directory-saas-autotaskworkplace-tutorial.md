---
title: "Tutorial: Integración de Azure Active Directory con Autotask Workplace | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Autotask al área de trabajo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="1ffc7-103">Tutorial: Integración de Azure Active Directory con Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="1ffc7-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="1ffc7-104">En este tutorial, aprenderá cómo toointegrate Autotask al área de trabajo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ffc7-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ffc7-105">Integración Autotask al área de trabajo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1ffc7-106">Puede controlar en Azure AD que tenga acceso tooAutotask al área de trabajo</span><span class="sxs-lookup"><span data-stu-id="1ffc7-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="1ffc7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAutotask al área de trabajo (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffc7-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ffc7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1ffc7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1ffc7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ffc7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ffc7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1ffc7-110">Prerequisites</span></span>

<span data-ttu-id="1ffc7-111">integración de Azure AD con un área de trabajo de Autotask tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="1ffc7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffc7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ffc7-113">Una suscripción habilitada para inicio de sesión único en Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="1ffc7-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="1ffc7-114">Es necesario que sea administrador o superadministrador en Workplace.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="1ffc7-115">Debe tener una cuenta de administrador en hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="1ffc7-116">los usuarios de Hola que vaya a usar esta característica deben tener cuentas dentro de un área de trabajo y hello Azure AD y deben coincidir con sus direcciones de correo electrónico para ambos.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="1ffc7-117">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ffc7-118">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ffc7-119">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ffc7-120">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ffc7-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ffc7-121">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1ffc7-121">Scenario description</span></span>
<span data-ttu-id="1ffc7-122">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ffc7-123">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ffc7-124">Agregar un área de trabajo Autotask de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1ffc7-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="1ffc7-125">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffc7-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="1ffc7-126">Agregar un área de trabajo Autotask de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1ffc7-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="1ffc7-127">integración de hello tooconfigure Autotask área de trabajo en Azure AD, deberá tooadd Autotask al área de trabajo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1ffc7-128">**tooadd Autotask al área de trabajo desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1ffc7-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ffc7-129">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="1ffc7-131">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1ffc7-132">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-132">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="1ffc7-134">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="1ffc7-136">En el cuadro de búsqueda de hello, escriba **al área de trabajo de Autotask**, seleccione **al área de trabajo de Autotask** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de un área de trabajo Autotask Hola](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1ffc7-138">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffc7-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1ffc7-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Autotask Workplace con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1ffc7-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1ffc7-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el área de trabajo de Autotask es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="1ffc7-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el área de trabajo de Autotask debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="1ffc7-142">En lugar de trabajo Autotask, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1ffc7-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Autotask al área de trabajo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1ffc7-144">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1ffc7-145">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ffc7-146">**[Crear un usuario de prueba al área de trabajo de Autotask](#create-an-autotask-workplace-test-user)**  -toohave un equivalente de Britta Simon en lugar de trabajo de Autotask es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ffc7-147">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ffc7-148">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1ffc7-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffc7-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1ffc7-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de área de trabajo de Autotask.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="1ffc7-151">**inicio de sesión único en tooconfigure Azure AD con Autotask al área de trabajo, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1ffc7-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ffc7-152">En el portal de Azure, en Hola Hola **al área de trabajo de Autotask** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="1ffc7-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="1ffc7-156">Si desea que aplicación de hello tooconfigure en **IDP** inicia el modo, realizar Hola seguir pasos de hello **Autotask al área de trabajo dominio y las direcciones URL** sección:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Autotask Workplace para IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="1ffc7-158">a.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-158">a.</span></span> <span data-ttu-id="1ffc7-159">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="1ffc7-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="1ffc7-160">b.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-160">b.</span></span> <span data-ttu-id="1ffc7-161">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="1ffc7-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="1ffc7-162">Si desea tooconfigure aplicación de hello en **SP** modo iniciado, comprobación de **mostrar avanzadas de configuración de la URL** y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Autotask Workplace para SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="1ffc7-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="1ffc7-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1ffc7-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-165">These values are not real.</span></span> <span data-ttu-id="1ffc7-166">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1ffc7-167">Póngase en contacto con [equipo de soporte técnico de cliente al área de trabajo de Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="1ffc7-168">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="1ffc7-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1ffc7-170">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1ffc7-172">En una ventana del explorador web diferente, inicio de sesión tooWorkplace Online mediante Hola credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="1ffc7-173">Al configurar Hola IdP, un subdominio deberá toobe especificado.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="1ffc7-174">tooconfirm Hola correcto subdominio, tooWorkplace de inicio de sesión en línea.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="1ffc7-175">Una vez iniciada la sesión, asegúrese de subdominio de toohello nota en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="1ffc7-176">subdominio Hola forma parte de hello entre Hola "https://" y ".awp.autotask.net/" y debe ser nos, Europa, Canadá o Australia.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="1ffc7-177">Vaya demasiado**configuración** > **Single Sign-On** y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Configuración de inicio de sesión único de Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="1ffc7-179">a.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-179">a.</span></span> <span data-ttu-id="1ffc7-180">Seleccione hello **archivo de metadatos XML** opción y, a continuación, cargar hello **Metadata XML** descargado del portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="1ffc7-181">b.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-181">b.</span></span> <span data-ttu-id="1ffc7-182">Haga clic en **Enable SSO** (Habilitar SSO).</span><span class="sxs-lookup"><span data-stu-id="1ffc7-182">Click **Enable SSO**.</span></span>
    
    ![Aprobación de configuración de inicio de sesión único de Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="1ffc7-184">c.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-184">c.</span></span> <span data-ttu-id="1ffc7-185">Seleccione hello **puedo confirmar esta información es correcta y confianza este IdP** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="1ffc7-186">d.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-186">d.</span></span> <span data-ttu-id="1ffc7-187">Haga clic en **Approve** (Aprobar).</span><span class="sxs-lookup"><span data-stu-id="1ffc7-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="1ffc7-188">Si necesita ayuda con la configuración de área de trabajo de Autotask, consulte la sección [esta página](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget asistencia con la cuenta de empresa.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="1ffc7-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="1ffc7-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1ffc7-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1ffc7-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ffc7-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1ffc7-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffc7-192">Create an Azure AD test user</span></span>

<span data-ttu-id="1ffc7-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="1ffc7-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1ffc7-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ffc7-196">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1ffc7-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1ffc7-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1ffc7-202">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1ffc7-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1ffc7-204">a.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-204">a.</span></span> <span data-ttu-id="1ffc7-205">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ffc7-206">b.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-206">b.</span></span> <span data-ttu-id="1ffc7-207">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1ffc7-208">c.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-208">c.</span></span> <span data-ttu-id="1ffc7-209">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1ffc7-210">d.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-210">d.</span></span> <span data-ttu-id="1ffc7-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="1ffc7-212">Creación de un usuario de prueba de Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="1ffc7-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="1ffc7-213">En esta sección, creará un usuario llamado Britta Simon en Autotask.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="1ffc7-214">Trabaje con [equipo de soporte técnico al área de trabajo de Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) a los usuarios de tooadd Hola Hola plataforma Autotask al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1ffc7-215">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ffc7-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1ffc7-216">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAutotask al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="1ffc7-218">**tooassign Britta Simon tooAutotask al área de trabajo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1ffc7-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ffc7-219">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1ffc7-221">En la lista de aplicaciones de hello, seleccione **al área de trabajo de Autotask**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![vínculo al área de trabajo de Autotask en la lista de aplicaciones de Hola Hola](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="1ffc7-223">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="1ffc7-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-225">Click **Add** button.</span></span> <span data-ttu-id="1ffc7-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="1ffc7-228">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1ffc7-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ffc7-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1ffc7-231">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1ffc7-231">Test single sign-on</span></span>

<span data-ttu-id="1ffc7-232">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1ffc7-233">Al hacer clic en hello al área de trabajo Autotask el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Autotask al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1ffc7-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="1ffc7-234">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1ffc7-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ffc7-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1ffc7-235">Additional resources</span></span>

* [<span data-ttu-id="1ffc7-236">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ffc7-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ffc7-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1ffc7-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

