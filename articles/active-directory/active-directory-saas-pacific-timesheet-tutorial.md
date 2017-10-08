---
title: "Tutorial: Integración de Azure Active Directory con Pacific Timesheet | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y parte de horas del Pacífico."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 5fd57ff78a3a64c135f2de9895f4643b39e33bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="38611-103">Tutorial: Integración de Azure Active Directory con Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="38611-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="38611-104">En este tutorial, aprenderá cómo toointegrate Pacífico parte de horas con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38611-104">In this tutorial, you learn how toointegrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38611-105">Integración del Pacífico horas con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="38611-105">Integrating Pacific Timesheet with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="38611-106">Puede controlar en Azure AD que tenga acceso tooPacific parte de horas</span><span class="sxs-lookup"><span data-stu-id="38611-106">You can control in Azure AD who has access tooPacific Timesheet</span></span>
- <span data-ttu-id="38611-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPacific parte de horas (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38611-107">You can enable your users tooautomatically get signed-on tooPacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38611-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="38611-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="38611-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38611-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38611-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="38611-110">Prerequisites</span></span>

<span data-ttu-id="38611-111">tooconfigure integración de Azure AD con parte de horas del Pacífico, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="38611-111">tooconfigure Azure AD integration with Pacific Timesheet, you need hello following items:</span></span>

- <span data-ttu-id="38611-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38611-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38611-113">Una suscripción habilitada para el inicio de sesión único en Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="38611-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38611-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="38611-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38611-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="38611-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38611-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="38611-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38611-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38611-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38611-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="38611-118">Scenario description</span></span>
<span data-ttu-id="38611-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="38611-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38611-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="38611-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38611-121">Agregar Pacific horas desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="38611-121">Adding Pacific Timesheet from hello gallery</span></span>
2. <span data-ttu-id="38611-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38611-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-hello-gallery"></a><span data-ttu-id="38611-123">Agregar Pacific horas desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="38611-123">Adding Pacific Timesheet from hello gallery</span></span>
<span data-ttu-id="38611-124">integración de hello tooconfigure de parte de horas del Pacífico en Azure AD, deberá tooadd parte de horas de Pacífico de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="38611-124">tooconfigure hello integration of Pacific Timesheet into Azure AD, you need tooadd Pacific Timesheet from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="38611-125">**tooadd Pacífico parte de horas desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38611-125">**tooadd Pacific Timesheet from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="38611-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="38611-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38611-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="38611-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="38611-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="38611-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="38611-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38611-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="38611-133">En el cuadro de búsqueda de hello, escriba **parte de horas de Pacific**.</span><span class="sxs-lookup"><span data-stu-id="38611-133">In hello search box, type **Pacific Timesheet**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="38611-135">En el panel de resultados de hello, seleccione **parte de horas de Pacific**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="38611-135">In hello results panel, select **Pacific Timesheet**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38611-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38611-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38611-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pacific Timesheet con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="38611-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38611-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en parte de horas de Pacífico es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38611-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pacific Timesheet is tooa user in Azure AD.</span></span> <span data-ttu-id="38611-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en parte de horas de Pacific debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="38611-140">In other words, a link relationship between an Azure AD user and hello related user in Pacific Timesheet needs toobe established.</span></span>

<span data-ttu-id="38611-141">En parte de horas del Pacífico, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="38611-141">In Pacific Timesheet, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="38611-142">tooconfigure y prueba de inicio de sesión único en Azure AD con parte de horas del Pacífico, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="38611-142">tooconfigure and test Azure AD single sign-on with Pacific Timesheet, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="38611-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="38611-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="38611-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38611-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38611-145">**[Crear un usuario de prueba de parte de horas de Pacific](#creating-a-pacific-timesheet-test-user)**  -toohave un equivalente de Britta Simon en parte de horas de Pacífico es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="38611-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - toohave a counterpart of Britta Simon in Pacific Timesheet that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="38611-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="38611-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38611-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="38611-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38611-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38611-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38611-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de parte de horas del Pacífico.</span><span class="sxs-lookup"><span data-stu-id="38611-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="38611-150">**inicio de sesión único en tooconfigure Azure AD con parte de horas del Pacífico, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38611-150">**tooconfigure Azure AD single sign-on with Pacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="38611-151">En el portal de Azure, en Hola Hola **parte de horas de Pacific** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="38611-151">In hello Azure portal, on hello **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="38611-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="38611-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="38611-155">En hello **Pacífico horas dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="38611-155">On hello **Pacific Timesheet Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="38611-157">a.</span><span class="sxs-lookup"><span data-stu-id="38611-157">a.</span></span> <span data-ttu-id="38611-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="38611-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="38611-159">b.</span><span class="sxs-lookup"><span data-stu-id="38611-159">b.</span></span> <span data-ttu-id="38611-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="38611-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38611-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="38611-161">These values are not real.</span></span> <span data-ttu-id="38611-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="38611-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="38611-163">Póngase en contacto con [equipo de soporte técnico de parte de horas de Pacific](http://www.pacifictimesheet.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="38611-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) tooget these values.</span></span>
 
4. <span data-ttu-id="38611-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="38611-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="38611-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="38611-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38611-168">En hello **Pacífico horas configuración** sección, haga clic en **configurar horas de Pacific** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="38611-168">On hello **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="38611-169">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="38611-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="38611-171">tooconfigure inicio de sesión único en **parte de horas de Pacific** lado, necesita hello toosend descargado **certificado (Base64)**, **SAML Single Sign-On dirección URL del servicio**y  **Id. de entidad SAML** demasiado[equipo de soporte técnico de parte de horas de Pacific](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="38611-171">tooconfigure single sign-on on **Pacific Timesheet** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="38611-172">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="38611-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="38611-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="38611-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="38611-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="38611-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="38611-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38611-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38611-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38611-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="38611-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="38611-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="38611-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38611-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="38611-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="38611-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38611-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="38611-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38611-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="38611-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38611-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="38611-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38611-188">a.</span><span class="sxs-lookup"><span data-stu-id="38611-188">a.</span></span> <span data-ttu-id="38611-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38611-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38611-190">b.</span><span class="sxs-lookup"><span data-stu-id="38611-190">b.</span></span> <span data-ttu-id="38611-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38611-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38611-192">c.</span><span class="sxs-lookup"><span data-stu-id="38611-192">c.</span></span> <span data-ttu-id="38611-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="38611-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="38611-194">d.</span><span class="sxs-lookup"><span data-stu-id="38611-194">d.</span></span> <span data-ttu-id="38611-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="38611-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="38611-196">Crear un usuario de prueba de Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="38611-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="38611-197">En esta sección, creará el usuario Britta Simon en Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="38611-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="38611-198">Trabajar con [equipo de soporte técnico de parte de horas de Pacific](http://www.pacifictimesheet.com/support) toocreate un usuario en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="38611-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) toocreate a user in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="38611-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="38611-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="38611-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPacific parte de horas.</span><span class="sxs-lookup"><span data-stu-id="38611-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPacific Timesheet.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="38611-202">**tooassign Britta Simon tooPacific parte de horas, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38611-202">**tooassign Britta Simon tooPacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="38611-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="38611-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="38611-205">En la lista de aplicaciones de hello, seleccione **parte de horas de Pacific**.</span><span class="sxs-lookup"><span data-stu-id="38611-205">In hello applications list, select **Pacific Timesheet**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="38611-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="38611-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="38611-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="38611-209">Click **Add** button.</span></span> <span data-ttu-id="38611-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="38611-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="38611-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="38611-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="38611-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="38611-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38611-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="38611-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38611-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="38611-215">Testing single sign-on</span></span>

<span data-ttu-id="38611-216">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="38611-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="38611-217">Al hacer clic en icono de parte de horas de Pacific Hola Hola Panel de acceso, deberá obtener la aplicación de parte de horas de Pacific tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="38611-217">When you click hello Pacific Timesheet tile in hello Access Panel, you should get automatically signed-on tooyour Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38611-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="38611-218">Additional resources</span></span>

* [<span data-ttu-id="38611-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38611-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38611-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38611-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png

