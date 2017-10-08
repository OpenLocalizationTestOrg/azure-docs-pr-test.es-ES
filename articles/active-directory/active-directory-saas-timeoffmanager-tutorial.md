---
title: "Tutorial: Integración de Azure Active Directory con TimeOffManager | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="b4d80-103">Tutorial: Integración de Azure Active Directory con TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="b4d80-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="b4d80-104">En este tutorial, aprenderá cómo toointegrate TimeOffManager con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4d80-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4d80-105">Integración de TimeOffManager con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b4d80-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b4d80-106">Puede controlar en Azure AD que tenga acceso tooTimeOffManager</span><span class="sxs-lookup"><span data-stu-id="b4d80-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="b4d80-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTimeOffManager (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d80-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b4d80-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b4d80-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b4d80-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4d80-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4d80-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b4d80-110">Prerequisites</span></span>

<span data-ttu-id="b4d80-111">integración de Azure AD con TimeOffManager tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b4d80-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="b4d80-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b4d80-113">Una suscripción habilitada para inicio de sesión único en TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="b4d80-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4d80-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b4d80-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4d80-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b4d80-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4d80-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b4d80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4d80-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4d80-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4d80-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b4d80-118">Scenario description</span></span>
<span data-ttu-id="b4d80-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b4d80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4d80-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="b4d80-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4d80-121">Agregar TimeOffManager de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b4d80-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="b4d80-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d80-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="b4d80-123">Agregar TimeOffManager de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b4d80-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="b4d80-124">integración de hello tooconfigure de TimeOffManager en Azure AD, deberá tooadd TimeOffManager de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="b4d80-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b4d80-125">**tooadd TimeOffManager de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b4d80-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d80-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b4d80-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b4d80-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b4d80-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b4d80-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b4d80-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b4d80-133">En el cuadro de búsqueda de hello, escriba **TimeOffManager**, seleccione **TimeOffManager** desde el panel de resultados y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b4d80-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Incorporación desde la galería](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b4d80-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d80-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b4d80-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TimeOffManager utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b4d80-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4d80-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TimeOffManager es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4d80-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="b4d80-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TimeOffManager debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="b4d80-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="b4d80-139">En TimeOffManager, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d80-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b4d80-140">tooconfigure y prueba de inicio de sesión único en Azure AD con TimeOffManager, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b4d80-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b4d80-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="b4d80-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b4d80-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4d80-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4d80-143">**[Crear un usuario de prueba de TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave un equivalente de Britta Simon en TimeOffManager que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b4d80-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b4d80-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b4d80-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4d80-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b4d80-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b4d80-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d80-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b4d80-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="b4d80-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="b4d80-148">**inicio de sesión único en Azure AD tooconfigure con TimeOffManager, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b4d80-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d80-149">En el portal de Azure, en Hola Hola **TimeOffManager** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b4d80-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b4d80-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="b4d80-153">En hello **TimeOffManager dominio y las direcciones URL** sección, realice Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4d80-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Sección Dominio y direcciones URL de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="b4d80-155">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="b4d80-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b4d80-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="b4d80-156">This value is not real.</span></span> <span data-ttu-id="b4d80-157">Actualizar este valor con la dirección URL de respuesta real Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d80-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="b4d80-158">Puede obtener este valor de **inicio de sesión único en la página de configuración de** que se explica más adelante en el tutorial de Hola o póngase en contacto con [equipo de soporte técnico de TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4d80-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="b4d80-159">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b4d80-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="b4d80-161">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooTimeOffManger con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d80-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="b4d80-162">La aplicación TimeOffManger espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="b4d80-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="b4d80-163">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="b4d80-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="b4d80-164">![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "Atributos de token de SAML")</span><span class="sxs-lookup"><span data-stu-id="b4d80-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="b4d80-165">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="b4d80-165">Attribute Name</span></span> | <span data-ttu-id="b4d80-166">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="b4d80-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="b4d80-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="b4d80-167">Firstname</span></span> |<span data-ttu-id="b4d80-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="b4d80-168">User.givenname</span></span> |
    | <span data-ttu-id="b4d80-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="b4d80-169">Lastname</span></span> |<span data-ttu-id="b4d80-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="b4d80-170">User.surname</span></span> |
    | <span data-ttu-id="b4d80-171">Email</span><span class="sxs-lookup"><span data-stu-id="b4d80-171">Email</span></span> |<span data-ttu-id="b4d80-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="b4d80-172">User.mail</span></span> |
    
    <span data-ttu-id="b4d80-173">a.</span><span class="sxs-lookup"><span data-stu-id="b4d80-173">a.</span></span>  <span data-ttu-id="b4d80-174">Para cada fila de datos de tabla de hello anterior, haga clic en **Agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="b4d80-175">![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "Atributos de token de SAML")</span><span class="sxs-lookup"><span data-stu-id="b4d80-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="b4d80-176">![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "Atributos de token de SAML")</span><span class="sxs-lookup"><span data-stu-id="b4d80-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="b4d80-177">b.</span><span class="sxs-lookup"><span data-stu-id="b4d80-177">b.</span></span>  <span data-ttu-id="b4d80-178">Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="b4d80-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b4d80-179">c.</span><span class="sxs-lookup"><span data-stu-id="b4d80-179">c.</span></span>  <span data-ttu-id="b4d80-180">Hola **valor del atributo** cuadro de texto, valor de atributo seleccione Hola se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="b4d80-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="b4d80-181">d.</span><span class="sxs-lookup"><span data-stu-id="b4d80-181">d.</span></span>  <span data-ttu-id="b4d80-182">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="b4d80-183">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b4d80-183">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b4d80-185">En hello **configuración de TimeOffManager** sección, haga clic en **configurar TimeOffManager** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="b4d80-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b4d80-186">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="b4d80-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sección Configuración de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="b4d80-188">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="b4d80-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="b4d80-189">Vaya demasiado**cuenta \> opciones de cuenta \> configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="b4d80-190">![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="b4d80-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="b4d80-191">Hola **configuración de inicio de sesión único** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b4d80-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="b4d80-192">![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="b4d80-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="b4d80-193">a.</span><span class="sxs-lookup"><span data-stu-id="b4d80-193">a.</span></span> <span data-ttu-id="b4d80-194">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, pegue Hola certificado completo en **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="b4d80-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="b4d80-195">b.</span><span class="sxs-lookup"><span data-stu-id="b4d80-195">b.</span></span> <span data-ttu-id="b4d80-196">En **emisor Idp** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d80-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="b4d80-197">c.</span><span class="sxs-lookup"><span data-stu-id="b4d80-197">c.</span></span> <span data-ttu-id="b4d80-198">En **dirección URL del extremo IdP** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d80-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="b4d80-199">d.</span><span class="sxs-lookup"><span data-stu-id="b4d80-199">d.</span></span> <span data-ttu-id="b4d80-200">En **Aplicar SAML**, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="b4d80-201">e.</span><span class="sxs-lookup"><span data-stu-id="b4d80-201">e.</span></span> <span data-ttu-id="b4d80-202">En **Crear usuarios automáticamente**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="b4d80-203">f.</span><span class="sxs-lookup"><span data-stu-id="b4d80-203">f.</span></span> <span data-ttu-id="b4d80-204">En **Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d80-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="b4d80-205">g.</span><span class="sxs-lookup"><span data-stu-id="b4d80-205">g.</span></span> <span data-ttu-id="b4d80-206">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="b4d80-207">En **configuración de inicio de sesión único** Hola de copiar valor de la página **dirección URL del servicio de consumidor de aserción** y péguelo en hello **dirección URL de respuesta** cuadro de texto bajo **TimeOffManager Dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d80-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="b4d80-208">![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="b4d80-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="b4d80-209">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="b4d80-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b4d80-210">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d80-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b4d80-211">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4d80-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b4d80-212">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d80-212">Create an Azure AD test user</span></span>
<span data-ttu-id="b4d80-213">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="b4d80-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b4d80-215">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b4d80-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d80-216">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b4d80-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b4d80-218">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuarios y grupos --> Todos los usuarios](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b4d80-220">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d80-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b4d80-222">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="b4d80-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página del cuadro de diálogo Usuario](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b4d80-224">a.</span><span class="sxs-lookup"><span data-stu-id="b4d80-224">a.</span></span> <span data-ttu-id="b4d80-225">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b4d80-226">b.</span><span class="sxs-lookup"><span data-stu-id="b4d80-226">b.</span></span> <span data-ttu-id="b4d80-227">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b4d80-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b4d80-228">c.</span><span class="sxs-lookup"><span data-stu-id="b4d80-228">c.</span></span> <span data-ttu-id="b4d80-229">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b4d80-230">d.</span><span class="sxs-lookup"><span data-stu-id="b4d80-230">d.</span></span> <span data-ttu-id="b4d80-231">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="b4d80-232">Creación de un usuario de prueba de TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="b4d80-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="b4d80-233">En orden tooenable toolog de los usuarios de Azure AD en TimeOffManager, deben ser tooTimeOffManager aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="b4d80-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="b4d80-234">TimeOffManager admite aprovisionamiento de usuarios justo a tiempo.</span><span class="sxs-lookup"><span data-stu-id="b4d80-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="b4d80-235">No hay ningún elemento de acción para usted.</span><span class="sxs-lookup"><span data-stu-id="b4d80-235">There is no action item for you.</span></span>  

<span data-ttu-id="b4d80-236">los usuarios de Hola se agregan automáticamente durante el saludo primer inicio de sesión con el inicio de sesión único en.</span><span class="sxs-lookup"><span data-stu-id="b4d80-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="b4d80-237">Puede usar cualquier otra TimeOffManager usuario cuenta herramienta de creación o las API proporcionadas por TimeOffManager tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4d80-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b4d80-238">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4d80-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b4d80-239">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="b4d80-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b4d80-241">**tooassign Britta Simon tooTimeOffManager, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b4d80-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4d80-242">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b4d80-244">En la lista de aplicaciones de hello, seleccione **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager en la lista de aplicaciones](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="b4d80-246">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b4d80-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-248">Click **Add** button.</span></span> <span data-ttu-id="b4d80-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b4d80-251">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d80-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b4d80-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b4d80-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b4d80-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b4d80-254">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="b4d80-254">Test single sign-on</span></span>

<span data-ttu-id="b4d80-255">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4d80-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b4d80-256">Al hacer clic en icono de TimeOffManager Hola Hola Panel de acceso, deberá obtener aplicaciones de TimeOffManager tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="b4d80-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="b4d80-257">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b4d80-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4d80-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b4d80-258">Additional resources</span></span>

* [<span data-ttu-id="b4d80-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4d80-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4d80-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4d80-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

