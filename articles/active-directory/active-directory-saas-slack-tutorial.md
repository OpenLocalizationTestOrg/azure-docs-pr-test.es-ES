---
title: "Tutorial: Integración de Azure Active Directory con Slack | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y demora."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="4a0e0-103">Tutorial: Integración de Azure Active Directory con Slack</span><span class="sxs-lookup"><span data-stu-id="4a0e0-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="4a0e0-104">En este tutorial, aprenderá cómo toointegrate una demora con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a0e0-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a0e0-105">Integración de demora con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a0e0-106">Puede controlar en Azure AD que tenga acceso tooSlack</span><span class="sxs-lookup"><span data-stu-id="4a0e0-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="4a0e0-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSlack (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a0e0-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a0e0-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4a0e0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4a0e0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a0e0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a0e0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4a0e0-110">Prerequisites</span></span>

<span data-ttu-id="4a0e0-111">integración de Azure AD con demora tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="4a0e0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a0e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a0e0-113">Una suscripción habilitada para el inicio de sesión único en Slack</span><span class="sxs-lookup"><span data-stu-id="4a0e0-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a0e0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a0e0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a0e0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a0e0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a0e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a0e0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4a0e0-118">Scenario description</span></span>
<span data-ttu-id="4a0e0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a0e0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a0e0-121">Agregar demora de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4a0e0-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="4a0e0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a0e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="4a0e0-123">Agregar demora de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4a0e0-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="4a0e0-124">integración de hello tooconfigure de demora en Azure AD, deberá tooadd demora de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a0e0-125">**tooadd demora de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a0e0-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a0e0-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4a0e0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a0e0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4a0e0-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4a0e0-133">En el cuadro de búsqueda de hello, escriba **Slack**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-133">In hello search box, type **Slack**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="4a0e0-135">En el panel de resultados de hello, seleccione **Slack**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a0e0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a0e0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a0e0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Slack con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4a0e0-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a0e0-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Slack es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="4a0e0-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en demora debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="4a0e0-141">En Slack, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4a0e0-142">tooconfigure y prueba de inicio de sesión único en Azure AD con demora, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a0e0-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a0e0-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a0e0-145">**[Crear un usuario de prueba demora](#creating-a-slack-test-user)**  -toohave un equivalente de Britta Simon en demora que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a0e0-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a0e0-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a0e0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a0e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a0e0-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de la demora.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="4a0e0-150">**inicio de sesión único en Azure AD tooconfigure con demora, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a0e0-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a0e0-151">En el portal de Azure, en Hola Hola **Slack** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4a0e0-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="4a0e0-155">En hello **demora de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="4a0e0-157">a.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-157">a.</span></span> <span data-ttu-id="4a0e0-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="4a0e0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="4a0e0-159">b.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-159">b.</span></span> <span data-ttu-id="4a0e0-160">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="4a0e0-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a0e0-161">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-161">hello value is not real.</span></span> <span data-ttu-id="4a0e0-162">Tiene valor de hello tooupdate con Hola inicio de sesión en dirección URL real.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="4a0e0-163">Póngase en contacto con [equipo de soporte técnico demora](https://slack.com/help/contact) valor de hello tooget</span><span class="sxs-lookup"><span data-stu-id="4a0e0-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="4a0e0-164">Aplicación demora espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4a0e0-165">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="4a0e0-166">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="4a0e0-167">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="4a0e0-169">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, seleccione **user.mail** como **identificador de usuario** y para cada fila se muestra en la tabla de Hola a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="4a0e0-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="4a0e0-170">Attribute Name</span></span> | <span data-ttu-id="4a0e0-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="4a0e0-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="4a0e0-172">first_name</span><span class="sxs-lookup"><span data-stu-id="4a0e0-172">first_name</span></span> | <span data-ttu-id="4a0e0-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4a0e0-173">user.givenname</span></span> |
    | <span data-ttu-id="4a0e0-174">last_name</span><span class="sxs-lookup"><span data-stu-id="4a0e0-174">last_name</span></span> | <span data-ttu-id="4a0e0-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="4a0e0-175">user.surname</span></span> |
    | <span data-ttu-id="4a0e0-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="4a0e0-176">User.Email</span></span> | <span data-ttu-id="4a0e0-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="4a0e0-177">user.mail</span></span> |  
    | <span data-ttu-id="4a0e0-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="4a0e0-178">User.Username</span></span> | <span data-ttu-id="4a0e0-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="4a0e0-179">user.userprincipalname</span></span> |

    <span data-ttu-id="4a0e0-180">a.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-180">a.</span></span> <span data-ttu-id="4a0e0-181">Haga clic en **atributo** tooopen **Editar atributo** diálogo cuadro y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="4a0e0-183">a.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-183">a.</span></span> <span data-ttu-id="4a0e0-184">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4a0e0-185">b.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-185">b.</span></span> <span data-ttu-id="4a0e0-186">De hello **valor** lista, el valor del atributo seleccione Hola se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4a0e0-187">c.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-187">c.</span></span> <span data-ttu-id="4a0e0-188">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="4a0e0-188">Click **OK**</span></span>

6. <span data-ttu-id="4a0e0-189">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="4a0e0-191">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4a0e0-191">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4a0e0-193">En hello **configuración de Slack** sección, haga clic en **configurar demora** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4a0e0-194">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="4a0e0-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="4a0e0-196">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de Slack tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="4a0e0-197">Navegue demasiado**Microsoft Azure AD** , a continuación, vaya demasiado**configuración del equipo**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="4a0e0-199">Hola **configuración del equipo** sección, haga clic en hello **autenticación** ficha y, a continuación, haga clic en **cambiar la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="4a0e0-201">En hello **SAML Authentication Settings** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="4a0e0-203">a.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-203">a.</span></span>  <span data-ttu-id="4a0e0-204">Hola **SAML 2.0 punto de conexión (HTTP)** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4a0e0-205">b.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-205">b.</span></span>  <span data-ttu-id="4a0e0-206">Hola **emisor del proveedor de identidades** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4a0e0-207">c.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-207">c.</span></span>  <span data-ttu-id="4a0e0-208">Abra el archivo de certificado descargado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado público** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="4a0e0-209">d.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-209">d.</span></span> <span data-ttu-id="4a0e0-210">Configurar Hola por encima de tres opciones de configuración según corresponda para su equipo demora.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="4a0e0-211">Para obtener más información acerca de la configuración de hello, podrá encontrar Hola **Guía de configuración de SSO de demora** aquí.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="4a0e0-212">e.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-212">e.</span></span>  <span data-ttu-id="4a0e0-213">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="4a0e0-214">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4a0e0-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4a0e0-215">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4a0e0-216">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a0e0-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a0e0-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a0e0-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a0e0-218">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4a0e0-220">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a0e0-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a0e0-221">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a0e0-223">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a0e0-225">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a0e0-227">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4a0e0-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a0e0-229">a.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-229">a.</span></span> <span data-ttu-id="4a0e0-230">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a0e0-231">b.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-231">b.</span></span> <span data-ttu-id="4a0e0-232">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a0e0-233">c.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-233">c.</span></span> <span data-ttu-id="4a0e0-234">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a0e0-235">d.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-235">d.</span></span> <span data-ttu-id="4a0e0-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="4a0e0-237">Creación de usuario de prueba de Slack</span><span class="sxs-lookup"><span data-stu-id="4a0e0-237">Creating a Slack test user</span></span>

<span data-ttu-id="4a0e0-238">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Slack.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="4a0e0-239">Slack admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4a0e0-240">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-240">There is no action item for you in this section.</span></span> <span data-ttu-id="4a0e0-241">Si no existe todavía, se crea un usuario nuevo durante un tooaccess de intento de demora.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0e0-242">Si necesita un usuario toocreate manualmente, necesita tooContact [equipo de soporte técnico demora](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="4a0e0-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4a0e0-243">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a0e0-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4a0e0-244">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSlack.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4a0e0-246">**tooassign Britta Simon tooSlack, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4a0e0-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a0e0-247">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4a0e0-249">En la lista de aplicaciones de hello, seleccione **Slack**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-249">In hello applications list, select **Slack**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="4a0e0-251">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4a0e0-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-253">Click **Add** button.</span></span> <span data-ttu-id="4a0e0-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4a0e0-256">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a0e0-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a0e0-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a0e0-259">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4a0e0-259">Testing single sign-on</span></span>

<span data-ttu-id="4a0e0-260">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4a0e0-261">Al hacer clic en el icono de demora de hello en Hola Panel de acceso, deberá obtener la aplicación demora tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="4a0e0-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a0e0-262">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4a0e0-262">Additional resources</span></span>

* [<span data-ttu-id="4a0e0-263">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a0e0-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a0e0-264">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a0e0-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

