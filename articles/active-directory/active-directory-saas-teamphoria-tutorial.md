---
title: "Tutorial: Integración de Azure Active Directory con Teamphoria | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="c2838-103">Tutorial: Integración de Azure Active Directory con Teamphoria</span><span class="sxs-lookup"><span data-stu-id="c2838-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="c2838-104">En este tutorial, aprenderá cómo toointegrate Teamphoria con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2838-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2838-105">Integración Teamphoria con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c2838-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c2838-106">Puede controlar en Azure AD que tenga acceso tooTeamphoria</span><span class="sxs-lookup"><span data-stu-id="c2838-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="c2838-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTeamphoria (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2838-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c2838-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="c2838-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="c2838-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c2838-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="c2838-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c2838-110">Prerequisites</span></span>

<span data-ttu-id="c2838-111">integración de Azure AD con Teamphoria tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c2838-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="c2838-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2838-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c2838-113">Una suscripción habilitada para el inicio de sesión único en Teamphoria</span><span class="sxs-lookup"><span data-stu-id="c2838-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2838-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c2838-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2838-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c2838-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2838-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c2838-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c2838-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2838-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2838-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c2838-118">Scenario description</span></span>
<span data-ttu-id="c2838-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c2838-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2838-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c2838-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2838-121">Agregar Teamphoria desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c2838-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="c2838-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2838-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="c2838-123">Agregar Teamphoria desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c2838-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="c2838-124">integración de hello tooconfigure de Teamphoria en Azure AD, deberá tooadd Teamphoria de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c2838-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c2838-125">**tooadd Teamphoria de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c2838-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2838-126">Hola ** [Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c2838-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c2838-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c2838-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c2838-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c2838-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c2838-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2838-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c2838-133">En el cuadro de búsqueda de hello, escriba **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="c2838-133">In hello search box, type **Teamphoria**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="c2838-135">En el panel de resultados de hello, seleccione **Teamphoria**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c2838-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c2838-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2838-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c2838-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Teamphoria con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c2838-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c2838-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Teamphoria es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2838-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="c2838-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Teamphoria debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c2838-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="c2838-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="c2838-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="c2838-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Teamphoria, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c2838-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c2838-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c2838-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c2838-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2838-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2838-145">**[Crear un usuario de prueba Teamphoria](#creating-a-teamphoria-test-user) ** -toohave un equivalente de Britta Simon en Teamphoria que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="c2838-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c2838-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c2838-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2838-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c2838-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c2838-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2838-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c2838-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="c2838-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="c2838-150">**inicio de sesión único en Azure AD tooconfigure con Teamphoria, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c2838-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2838-151">En el portal de administración de Azure de hello, en hello **Teamphoria** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c2838-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c2838-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c2838-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="c2838-155">En hello **Teamphoria dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c2838-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="c2838-157">a.</span><span class="sxs-lookup"><span data-stu-id="c2838-157">a.</span></span> <span data-ttu-id="c2838-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL con hello sigue el patrón:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="c2838-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="c2838-159">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2838-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="c2838-160">Tiene estos valores con hello tooupdate dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="c2838-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="c2838-161">Póngase en contacto con [equipo de soporte técnico de cliente de Teamphoria](https://www.teamphoria.com/) tooget Hola sesión URL.</span><span class="sxs-lookup"><span data-stu-id="c2838-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="c2838-162">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c2838-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="c2838-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c2838-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c2838-166">En hello **Teamphoria configuración** sección, haga clic en **configurar Teamphoria** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c2838-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c2838-167">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c2838-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="c2838-169">inicio de sesión único en tooconfigure en **Teamphoria** lado, la aplicación de Teamphoria tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="c2838-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="c2838-170">Vaya demasiado**configuración de administración** opción en la barra de herramientas izquierda hello y en Hola Hola ficha configurar, haga clic en **inicio de sesión único** ventana de configuración de SSO de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="c2838-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="c2838-172">Haga clic en **Agregar nuevo proveedor de IDENTIDADES** opción en forma de Hola de tooopen Hola esquina superior derecha para agregar una configuración de Hola para SSO.</span><span class="sxs-lookup"><span data-stu-id="c2838-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="c2838-174">Escriba los detalles de hello en campos de hello tal como se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="c2838-174">Enter hello details in hello fields as described below-</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="c2838-176">a.</span><span class="sxs-lookup"><span data-stu-id="c2838-176">a.</span></span> <span data-ttu-id="c2838-177">**NOMBRE para mostrar** : escriba el nombre para mostrar hello de complemento de hello en la página de administración Hola.</span><span class="sxs-lookup"><span data-stu-id="c2838-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="c2838-178">b.</span><span class="sxs-lookup"><span data-stu-id="c2838-178">b.</span></span> <span data-ttu-id="c2838-179">**NOMBRE del botón** : nombre de Hola de pestaña de Hola que se mostrará en la página de inicio de sesión de hello para el inicio de sesión mediante SSO.</span><span class="sxs-lookup"><span data-stu-id="c2838-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="c2838-180">c.</span><span class="sxs-lookup"><span data-stu-id="c2838-180">c.</span></span> <span data-ttu-id="c2838-181">**CERTIFICADO** : Hola abierto certificado descargó anteriormente desde el portal de Azure en el Bloc de notas, copie el contenido de Hola Hola Hola igual y péguelo aquí en el cuadro de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2838-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="c2838-182">d.</span><span class="sxs-lookup"><span data-stu-id="c2838-182">d.</span></span> <span data-ttu-id="c2838-183">**PUNTO de entrada** : Hola pegar **SAML Single Sign-On dirección URL del servicio** copian Hola de formulario anterior portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2838-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="c2838-184">e.</span><span class="sxs-lookup"><span data-stu-id="c2838-184">e.</span></span> <span data-ttu-id="c2838-185">Cambiar la opción de hello demasiado**ON** y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c2838-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c2838-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2838-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c2838-187">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c2838-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c2838-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c2838-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2838-190">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c2838-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c2838-192">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c2838-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c2838-194">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c2838-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c2838-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c2838-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c2838-198">a.</span><span class="sxs-lookup"><span data-stu-id="c2838-198">a.</span></span> <span data-ttu-id="c2838-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2838-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2838-200">b.</span><span class="sxs-lookup"><span data-stu-id="c2838-200">b.</span></span> <span data-ttu-id="c2838-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c2838-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c2838-202">c.</span><span class="sxs-lookup"><span data-stu-id="c2838-202">c.</span></span> <span data-ttu-id="c2838-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c2838-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c2838-204">d.</span><span class="sxs-lookup"><span data-stu-id="c2838-204">d.</span></span> <span data-ttu-id="c2838-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c2838-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="c2838-206">Crear un usuario de prueba Teamphoria</span><span class="sxs-lookup"><span data-stu-id="c2838-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="c2838-207">En orden tooenable toolog de los usuarios de Azure AD en Teamphoria, se les deben aprovisionar en Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="c2838-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="c2838-208">En caso de hello de Teamphoria, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="c2838-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="c2838-209">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="c2838-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2838-210">Inicie sesión en tooyour Teamphoria sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="c2838-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="c2838-211">Haga clic en **administración** parámetros en la barra de herramientas izquierda hello y en hello **administrar** pestaña haga clic en **usuarios** tooopen página de administración de Hola para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c2838-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Agregar empleado](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="c2838-213">Haga clic en hello **invitar a MANUAL** opción.</span><span class="sxs-lookup"><span data-stu-id="c2838-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="c2838-215">En esta página, realizar las acciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="c2838-215">On this page, perform following action.</span></span> 
    
    ![Invitar a contactos](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="c2838-217">a.</span><span class="sxs-lookup"><span data-stu-id="c2838-217">a.</span></span> <span data-ttu-id="c2838-218">Hola **dirección de correo electrónico** cuadro de texto, hello **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c2838-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c2838-219">b.</span><span class="sxs-lookup"><span data-stu-id="c2838-219">b.</span></span> <span data-ttu-id="c2838-220">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="c2838-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="c2838-221">c.</span><span class="sxs-lookup"><span data-stu-id="c2838-221">c.</span></span> <span data-ttu-id="c2838-222">Hola **LAST NAME** cuadro de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c2838-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="c2838-223">d.</span><span class="sxs-lookup"><span data-stu-id="c2838-223">d.</span></span> <span data-ttu-id="c2838-224">Haga clic en **INVITE 1 USER**.</span><span class="sxs-lookup"><span data-stu-id="c2838-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="c2838-225">El usuario necesita tooaccept Hola invitación tooget creado en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2838-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c2838-226">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2838-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c2838-227">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooTeamphoria de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2838-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c2838-229">**tooassign Britta Simon tooTeamphoria, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c2838-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2838-230">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c2838-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c2838-232">En la lista de aplicaciones de hello, seleccione **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="c2838-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="c2838-234">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c2838-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c2838-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c2838-236">Click **Add** button.</span></span> <span data-ttu-id="c2838-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c2838-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c2838-239">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2838-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c2838-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c2838-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c2838-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c2838-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c2838-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c2838-242">Testing single sign-on</span></span>

<span data-ttu-id="c2838-243">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2838-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c2838-244">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2838-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c2838-245">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c2838-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c2838-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c2838-246">Additional resources</span></span>

* [<span data-ttu-id="c2838-247">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2838-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2838-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c2838-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

