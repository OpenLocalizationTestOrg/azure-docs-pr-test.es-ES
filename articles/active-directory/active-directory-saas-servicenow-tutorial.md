---
title: "Tutorial: Integración de Azure Active Directory con ServiceNow | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ServiceNow y ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="c34de-103">Tutorial: Integración de Azure Active Directory con ServiceNow</span><span class="sxs-lookup"><span data-stu-id="c34de-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="c34de-104">En este tutorial, aprenderá cómo toointegrate ServiceNow y ServiceNow Express con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c34de-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c34de-105">Integración de ServiceNow y ServiceNow Express con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c34de-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="c34de-106">Puede controlar en Azure AD que tenga acceso tooServiceNow y ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="c34de-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="c34de-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooServiceNow y ServiceNow Express (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c34de-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="c34de-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="c34de-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="c34de-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c34de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c34de-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c34de-110">Prerequisites</span></span>
<span data-ttu-id="c34de-111">integración de Azure AD con ServiceNow y ServiceNow Express tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c34de-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="c34de-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c34de-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c34de-113">Para ServiceNow, una instancia o inquilino de ServiceNow, versión Calgary o superior</span><span class="sxs-lookup"><span data-stu-id="c34de-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="c34de-114">Para ServiceNow Express, una instancia de ServiceNow Express, versión Helsinki o superior</span><span class="sxs-lookup"><span data-stu-id="c34de-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="c34de-115">inquilino de ServiceNow Hola debe tener hello [varios único inicio de sesión de complemento de proveedor de](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) habilitado.</span><span class="sxs-lookup"><span data-stu-id="c34de-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="c34de-116">Esto puede hacerse [enviando una solicitud de servicio](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="c34de-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="c34de-117">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c34de-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="c34de-118">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c34de-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c34de-119">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c34de-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c34de-120">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c34de-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c34de-121">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c34de-121">Scenario description</span></span>
<span data-ttu-id="c34de-122">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c34de-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c34de-123">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c34de-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c34de-124">Agregar ServiceNow desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c34de-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="c34de-125">Configuración y comprobación del inicio de sesión único de Azure AD en ServiceNow o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="c34de-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="c34de-126">Agregar ServiceNow desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c34de-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="c34de-127">integración de hello tooconfigure de ServiceNow o ServiceNow Express en Azure AD, deberá tooadd ServiceNow de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c34de-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="c34de-128">**tooadd ServiceNow de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c34de-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c34de-129">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c34de-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="c34de-131">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="c34de-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="c34de-132">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="c34de-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicaciones][2]
4. <span data-ttu-id="c34de-134">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="c34de-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="c34de-136">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="c34de-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicaciones][4]
6. <span data-ttu-id="c34de-138">En el cuadro de búsqueda de hello, escriba **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="c34de-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="c34de-140">En el panel de resultados de hello, seleccione **ServiceNow**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c34de-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c34de-142">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c34de-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c34de-143">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ServiceNow o ServiceNow con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c34de-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c34de-144">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ServiceNow es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c34de-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="c34de-145">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ServiceNow debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c34de-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="c34de-146">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="c34de-147">tooconfigure y prueba de inicio de sesión único en Azure AD con ServiceNow, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c34de-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c34de-148">**[Configurar Azure AD Single Sign-On para ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c34de-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c34de-149">**[Configurar Azure AD Single Sign-On para ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c34de-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="c34de-150">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c34de-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="c34de-151">**[Crear un usuario de prueba de ServiceNow](#creating-a-servicenow-test-user)**  -toohave un equivalente de Britta Simon en ServiceNow que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="c34de-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="c34de-152">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c34de-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="c34de-153">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c34de-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="c34de-154">Si desea que tooconfigure ServiceNow omite el paso 2.</span><span class="sxs-lookup"><span data-stu-id="c34de-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="c34de-155">Del mismo modo, si desea tooconfigure ServiceNow Express, que omite el paso 1.</span><span class="sxs-lookup"><span data-stu-id="c34de-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="c34de-156">Configuración del inicio de sesión único de Azure AD para ServiceNow</span><span class="sxs-lookup"><span data-stu-id="c34de-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="c34de-157">En portal clásico de hello Azure AD, en hello **ServiceNow** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo .</span><span class="sxs-lookup"><span data-stu-id="c34de-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="c34de-158">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="c34de-159">En hello **¿cómo desea que los usuarios toosign en tooServiceNow** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c34de-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="c34de-160">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="c34de-161">En hello **configurar opciones de aplicación** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c34de-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="c34de-162">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="c34de-163">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-163">a.</span></span> <span data-ttu-id="c34de-164">Hola **ServiceNow inicio de sesión en la URL** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="c34de-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="c34de-165">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-165">b.</span></span> <span data-ttu-id="c34de-166">Hola **identificador** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="c34de-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="c34de-167">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-167">c.</span></span> <span data-ttu-id="c34de-168">Haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="c34de-168">Click **Next**</span></span>

4. <span data-ttu-id="c34de-169">toohave Azure AD automáticamente configurar ServiceNow para la autenticación de SAML, escriba el nombre de instancia de ServiceNow, nombre de usuario y contraseña de administrador en hello **configuración automática de inicio de sesión único** formulario y haga clic en  *Configurar*.</span><span class="sxs-lookup"><span data-stu-id="c34de-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="c34de-170">Tenga en cuenta ese nombre de usuario de administrador Hola proporcionado debe tener hello **security_admin** rol asignado en ServiceNow para este toowork.</span><span class="sxs-lookup"><span data-stu-id="c34de-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="c34de-171">En caso contrario, toomanually configurar ServiceNow toouse Azure AD como proveedor de identidades SAML, haga clic en **configurar manualmente la aplicación hello para el inicio de sesión único**, a continuación, haga clic en **siguiente** hello completa y pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="c34de-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="c34de-172">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="c34de-173">En hello **configurar inicio de sesión único en ServiceNow** página, haga clic en **Descargar certificado**, guardar el archivo de certificado de hello localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c34de-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="c34de-174">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="c34de-175">Inicio de sesión tooyour ServiceNow aplicación como administrador.</span><span class="sxs-lookup"><span data-stu-id="c34de-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="c34de-176">Activar hello *integración - varios Single Sign-On instalador de proveedor* complemento siguiendo Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c34de-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="c34de-177">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-177">a.</span></span> <span data-ttu-id="c34de-178">En el panel de navegación de hello en el lado izquierdo de hello, vaya demasiado**definición del sistema** sección y, a continuación, haga clic en **complementos**.</span><span class="sxs-lookup"><span data-stu-id="c34de-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="c34de-179">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")(Activar complemento)</span><span class="sxs-lookup"><span data-stu-id="c34de-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="c34de-180">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-180">b.</span></span> <span data-ttu-id="c34de-181">Busque *Integration - Multiple Provider Single Sign-On Installer*.</span><span class="sxs-lookup"><span data-stu-id="c34de-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="c34de-182">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")(Activar complemento)</span><span class="sxs-lookup"><span data-stu-id="c34de-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="c34de-183">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-183">c.</span></span> <span data-ttu-id="c34de-184">Seleccione el complemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="c34de-184">Select hello plugin.</span></span> <span data-ttu-id="c34de-185">Haga clic con el botón derecho y seleccione **Activate/Upgrade** (Activar o actualizar).</span><span class="sxs-lookup"><span data-stu-id="c34de-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="c34de-186">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-186">d.</span></span> <span data-ttu-id="c34de-187">Haga clic en hello **activar** botón.</span><span class="sxs-lookup"><span data-stu-id="c34de-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="c34de-188">En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="c34de-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="c34de-189">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="c34de-190">En hello **varias propiedades de proveedor de SSO** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="c34de-191">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="c34de-192">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-192">a.</span></span> <span data-ttu-id="c34de-193">En **Enable multiple provider SSO** (Habilitar SSO de varios proveedores), seleccione **Yes** (Sí).</span><span class="sxs-lookup"><span data-stu-id="c34de-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="c34de-194">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-194">b.</span></span> <span data-ttu-id="c34de-195">Como **habilitar el registro de depuración se obtuvo Hola proveedor múltiples integración de SSO**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c34de-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="c34de-196">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-196">c.</span></span> <span data-ttu-id="c34de-197">En **campo hello en usuario Hola de tabla que...**  cuadro de texto, tipo **nombre_usuario**.</span><span class="sxs-lookup"><span data-stu-id="c34de-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="c34de-198">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-198">d.</span></span> <span data-ttu-id="c34de-199">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-199">Click **Save**.</span></span>

10. <span data-ttu-id="c34de-200">En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **x509 certificados**.</span><span class="sxs-lookup"><span data-stu-id="c34de-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="c34de-201">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="c34de-202">En hello **certificados X.509** cuadro de diálogo, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="c34de-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="c34de-203">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="c34de-204">En hello **certificados X.509** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="c34de-205">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="c34de-206">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-206">a.</span></span> <span data-ttu-id="c34de-207">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="c34de-207">Click **New**.</span></span>
    
     <span data-ttu-id="c34de-208">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-208">b.</span></span> <span data-ttu-id="c34de-209">Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="c34de-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="c34de-210">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-210">c.</span></span> <span data-ttu-id="c34de-211">Seleccione **Active**(Activo).</span><span class="sxs-lookup"><span data-stu-id="c34de-211">Select **Active**.</span></span>
    
     <span data-ttu-id="c34de-212">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-212">d.</span></span> <span data-ttu-id="c34de-213">En **Format** (Formato), seleccione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="c34de-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="c34de-214">e.</span><span class="sxs-lookup"><span data-stu-id="c34de-214">e.</span></span> <span data-ttu-id="c34de-215">En **Type** (Tipo), seleccione **Trust Store Cert** (Confiar en certificados de almacén).</span><span class="sxs-lookup"><span data-stu-id="c34de-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="c34de-216">f.</span><span class="sxs-lookup"><span data-stu-id="c34de-216">f.</span></span> <span data-ttu-id="c34de-217">Abra el certificado codificado en Base64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado PEM** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="c34de-218">g.</span><span class="sxs-lookup"><span data-stu-id="c34de-218">g.</span></span> <span data-ttu-id="c34de-219">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="c34de-219">Click **Update**.</span></span>

13. <span data-ttu-id="c34de-220">En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="c34de-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="c34de-221">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="c34de-222">En hello **proveedores de identidades** cuadro de diálogo, haga clic en **New**:</span><span class="sxs-lookup"><span data-stu-id="c34de-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="c34de-223">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="c34de-224">En hello **proveedores de identidades** cuadro de diálogo, haga clic en **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="c34de-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="c34de-225">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="c34de-226">En el cuadro de diálogo de propiedades de la actualización 1 de SAML2 hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="c34de-227">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c34de-228">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-228">a.</span></span> <span data-ttu-id="c34de-229">Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="c34de-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="c34de-230">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-230">b.</span></span> <span data-ttu-id="c34de-231">Hola **campo usuario** cuadro de texto, tipo **correo electrónico** o **nombre_usuario**, dependiendo de qué campo se usa toouniquely identificar a los usuarios en la implementación de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="c34de-232">Puede configue Azure AD tooemit cualquier Id. de usuario de hello Azure AD (nombre principal de usuario) u Hola dirección de correo electrónico como Hola identificador único en el token SAML de Hola por van toohello **ServiceNow > atributos > Single Sign-On** sección de Hola portal de Azure clásico y asignación Hola deseado campo toohello **nameidentifier** atributo.</span><span class="sxs-lookup"><span data-stu-id="c34de-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="c34de-233">Hola valor almacenado para el atributo seleccionado hello en Azure AD (p. ej. nombre principal de usuario) debe coincidir con hello almacenados en ServiceNow para el campo de hello especificado (por ejemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="c34de-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="c34de-234">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-234">c.</span></span> <span data-ttu-id="c34de-235">En el portal clásico de hello Azure AD, copie hello **Id. de proveedor de identidad** valor y, a continuación, péguelo en hello **dirección URL del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="c34de-236">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-236">d.</span></span> <span data-ttu-id="c34de-237">En el portal clásico de hello Azure AD, copie hello **URL de solicitud de autenticación** valor y, a continuación, péguelo en hello **AuthnRequest del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="c34de-238">e.</span><span class="sxs-lookup"><span data-stu-id="c34de-238">e.</span></span> <span data-ttu-id="c34de-239">En el portal clásico de hello Azure AD, copie hello **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **SingleLogoutRequest del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="c34de-240">f.</span><span class="sxs-lookup"><span data-stu-id="c34de-240">f.</span></span> <span data-ttu-id="c34de-241">Hola **ServiceNow Homepage** cuadro de texto, escriba Hola la dirección URL de la página de inicio de la instancia de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c34de-242">página de inicio de instancia de ServiceNow de Hello es una concatenación de su **dirección URL del inquilino ServieNow** y **/navpage.DO** (p. ej.:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="c34de-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="c34de-243">g.</span><span class="sxs-lookup"><span data-stu-id="c34de-243">g.</span></span> <span data-ttu-id="c34de-244">Hola **Id. de entidad / emisor** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="c34de-245">h.</span><span class="sxs-lookup"><span data-stu-id="c34de-245">h.</span></span> <span data-ttu-id="c34de-246">Hola **dirección URL de audiencia** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="c34de-247">i.</span><span class="sxs-lookup"><span data-stu-id="c34de-247">i.</span></span> <span data-ttu-id="c34de-248">Hola **protocolo de enlace de hello del IDP SingleLogoutRequest** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:bindings:HTTP-redirigir**.</span><span class="sxs-lookup"><span data-stu-id="c34de-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="c34de-249">j.</span><span class="sxs-lookup"><span data-stu-id="c34de-249">j.</span></span> <span data-ttu-id="c34de-250">En el cuadro de texto de política de NameID hello, escriba **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: sin especificar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="c34de-251">k.</span><span class="sxs-lookup"><span data-stu-id="c34de-251">k.</span></span> <span data-ttu-id="c34de-252">Anule la selección de **Create an AuthnContextClass**(Crear AuthnContextClass).</span><span class="sxs-lookup"><span data-stu-id="c34de-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="c34de-253">l.</span><span class="sxs-lookup"><span data-stu-id="c34de-253">l.</span></span> <span data-ttu-id="c34de-254">Hola **método AuthnContextClassRef**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="c34de-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="c34de-255">Esto solo es preciso para las organizaciones que solo trabajan en la nube.</span><span class="sxs-lookup"><span data-stu-id="c34de-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="c34de-256">Si se usa MFA o ADFS local para la autenticación, este valor no se debe configurar.</span><span class="sxs-lookup"><span data-stu-id="c34de-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="c34de-257">m.</span><span class="sxs-lookup"><span data-stu-id="c34de-257">m.</span></span> <span data-ttu-id="c34de-258">En el cuadro de diálogo **Clock Skew** (Desplazamiento del reloj), escriba **60**.</span><span class="sxs-lookup"><span data-stu-id="c34de-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="c34de-259">n.</span><span class="sxs-lookup"><span data-stu-id="c34de-259">n.</span></span> <span data-ttu-id="c34de-260">En **Single Sign On Script** (Script de inicio de sesión único), seleccione **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="c34de-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="c34de-261">o.</span><span class="sxs-lookup"><span data-stu-id="c34de-261">o.</span></span> <span data-ttu-id="c34de-262">Como **x509 certificado**, seleccione certificado Hola ha creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="c34de-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="c34de-263">p.</span><span class="sxs-lookup"><span data-stu-id="c34de-263">p.</span></span> <span data-ttu-id="c34de-264">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="c34de-265">En el portal clásico de hello Azure AD, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c34de-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="c34de-266">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="c34de-267">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="c34de-268">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="c34de-269">Configuración del inicio de sesión único de Azure AD para ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="c34de-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="c34de-270">En portal clásico de hello Azure AD, en hello **ServiceNow** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo .</span><span class="sxs-lookup"><span data-stu-id="c34de-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="c34de-271">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="c34de-272">En hello **¿cómo desea que los usuarios toosign en tooServiceNow** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c34de-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="c34de-273">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="c34de-274">En hello **configurar opciones de aplicación** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c34de-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="c34de-275">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="c34de-276">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-276">a.</span></span> <span data-ttu-id="c34de-277">Hola **ServiceNow inicio de sesión en la URL** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="c34de-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="c34de-278">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-278">b.</span></span> <span data-ttu-id="c34de-279">Hola **dirección URL del emisor** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="c34de-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="c34de-280">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-280">c.</span></span> <span data-ttu-id="c34de-281">Haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="c34de-281">Click **Next**</span></span>

4. <span data-ttu-id="c34de-282">Haga clic en **configurar manualmente la aplicación hello para el inicio de sesión único**, a continuación, haga clic en **siguiente** y Hola completa siguiendo los pasos indicados.</span><span class="sxs-lookup"><span data-stu-id="c34de-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="c34de-283">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="c34de-284">En hello **configurar inicio de sesión único en ServiceNow** página, haga clic en **Descargar certificado**, guardar el archivo de certificado de hello localmente en el equipo y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c34de-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="c34de-285">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="c34de-286">Inicio de sesión tooyour ServiceNow Express aplicación como administrador.</span><span class="sxs-lookup"><span data-stu-id="c34de-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="c34de-287">En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c34de-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="c34de-288">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="c34de-289">En hello **Single Sign-On** cuadro de diálogo, haga clic en el icono de configuración de hello en superior de hello derecho y establezca hello siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="c34de-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="c34de-290">![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c34de-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="c34de-291">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-291">a.</span></span> <span data-ttu-id="c34de-292">Alternar **habilitar proveedor múltiples SSO** toohello derecha.</span><span class="sxs-lookup"><span data-stu-id="c34de-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="c34de-293">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-293">b.</span></span> <span data-ttu-id="c34de-294">Alternar **depuración Habilitar registro de hello proveedor múltiples integración de SSO** toohello derecha.</span><span class="sxs-lookup"><span data-stu-id="c34de-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="c34de-295">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-295">c.</span></span> <span data-ttu-id="c34de-296">En **campo hello en usuario Hola de tabla que...**  cuadro de texto, tipo **nombre_usuario**.</span><span class="sxs-lookup"><span data-stu-id="c34de-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="c34de-297">En hello **Single Sign-On** cuadro de diálogo, haga clic en **Agregar nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="c34de-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="c34de-298">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="c34de-299">En hello **certificados X.509** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="c34de-300">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="c34de-301">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-301">a.</span></span> <span data-ttu-id="c34de-302">Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="c34de-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="c34de-303">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-303">b.</span></span> <span data-ttu-id="c34de-304">Seleccione **Active**(Activo).</span><span class="sxs-lookup"><span data-stu-id="c34de-304">Select **Active**.</span></span>
    
    <span data-ttu-id="c34de-305">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-305">c.</span></span> <span data-ttu-id="c34de-306">En **Format** (Formato), seleccione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="c34de-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="c34de-307">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-307">d.</span></span> <span data-ttu-id="c34de-308">En **Type** (Tipo), seleccione **Trust Store Cert** (Confiar en certificados de almacén).</span><span class="sxs-lookup"><span data-stu-id="c34de-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="c34de-309">e.</span><span class="sxs-lookup"><span data-stu-id="c34de-309">e.</span></span> <span data-ttu-id="c34de-310">Cree un archivo con codificación Base64 a partir del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="c34de-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c34de-311">Para obtener más información, consulte [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="c34de-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="c34de-312">f.</span><span class="sxs-lookup"><span data-stu-id="c34de-312">f.</span></span> <span data-ttu-id="c34de-313">Abra el certificado codificado en Base64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado PEM** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="c34de-314">g.</span><span class="sxs-lookup"><span data-stu-id="c34de-314">g.</span></span> <span data-ttu-id="c34de-315">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="c34de-315">Click **Update**.</span></span>
11. <span data-ttu-id="c34de-316">En hello **Single Sign-On** cuadro de diálogo, haga clic en **agregar nueva IdP**.</span><span class="sxs-lookup"><span data-stu-id="c34de-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="c34de-317">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="c34de-318">En hello **Agregar nuevo proveedor de identidades** cuadro de diálogo, en **configurar el proveedor de identidades**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="c34de-319">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c34de-320">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-320">a.</span></span> <span data-ttu-id="c34de-321">Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="c34de-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="c34de-322">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-322">b.</span></span> <span data-ttu-id="c34de-323">En el portal clásico de hello Azure AD, copie hello **Id. de proveedor de identidad** valor y, a continuación, péguelo en hello **dirección URL del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="c34de-324">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-324">c.</span></span> <span data-ttu-id="c34de-325">En el portal clásico de hello Azure AD, copie hello **URL de solicitud de autenticación** valor y, a continuación, péguelo en hello **AuthnRequest del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="c34de-326">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-326">d.</span></span> <span data-ttu-id="c34de-327">En el portal clásico de hello Azure AD, copie hello **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **SingleLogoutRequest del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c34de-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="c34de-328">e.</span><span class="sxs-lookup"><span data-stu-id="c34de-328">e.</span></span> <span data-ttu-id="c34de-329">Como **certificado del proveedor de identidad**, seleccione certificado Hola ha creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="c34de-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="c34de-330">Haga clic en **configuración avanzada**y en **propiedades adicionales del proveedor de identidad**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="c34de-331">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="c34de-332">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-332">a.</span></span> <span data-ttu-id="c34de-333">Hola **protocolo de enlace de hello del IDP SingleLogoutRequest** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:bindings:HTTP-redirigir**.</span><span class="sxs-lookup"><span data-stu-id="c34de-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="c34de-334">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-334">b.</span></span> <span data-ttu-id="c34de-335">Hola **política de NameID** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: sin especificar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="c34de-336">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-336">c.</span></span> <span data-ttu-id="c34de-337">Hola **método AuthnContextClassRef**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="c34de-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="c34de-338">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-338">d.</span></span> <span data-ttu-id="c34de-339">Anule la selección de **Create an AuthnContextClass**(Crear AuthnContextClass).</span><span class="sxs-lookup"><span data-stu-id="c34de-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="c34de-340">En **propiedades adicionales del proveedor de servicio**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="c34de-341">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="c34de-342">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-342">a.</span></span> <span data-ttu-id="c34de-343">Hola **ServiceNow Homepage** cuadro de texto, escriba Hola la dirección URL de la página de inicio de la instancia de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="c34de-344">página de inicio de instancia de ServiceNow de Hello es una concatenación de su **dirección URL del inquilino ServieNow** y **/navpage.DO** (p. ej.: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="c34de-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="c34de-345">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-345">b.</span></span> <span data-ttu-id="c34de-346">Hola **Id. de entidad / emisor** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="c34de-347">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-347">c.</span></span> <span data-ttu-id="c34de-348">Hola **URI de audiencia** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="c34de-349">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-349">d.</span></span> <span data-ttu-id="c34de-350">En el cuadro de diálogo **Clock Skew** (Desplazamiento del reloj), escriba **60**.</span><span class="sxs-lookup"><span data-stu-id="c34de-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="c34de-351">e.</span><span class="sxs-lookup"><span data-stu-id="c34de-351">e.</span></span> <span data-ttu-id="c34de-352">Hola **campo usuario** cuadro de texto, tipo **correo electrónico** o **nombre_usuario**, dependiendo de qué campo se usa toouniquely identificar a los usuarios en la implementación de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="c34de-353">Puede configue Azure AD tooemit cualquier Id. de usuario de hello Azure AD (nombre principal de usuario) u Hola dirección de correo electrónico como Hola identificador único en el token SAML de Hola por van toohello **ServiceNow > atributos > Single Sign-On** sección de Hola portal de Azure clásico y asignación Hola deseado campo toohello **nameidentifier** atributo.</span><span class="sxs-lookup"><span data-stu-id="c34de-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="c34de-354">Hola valor almacenado para el atributo seleccionado hello en Azure AD (p. ej. nombre principal de usuario) debe coincidir con hello almacenados en ServiceNow para el campo de hello especificado (por ejemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="c34de-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="c34de-355">f.</span><span class="sxs-lookup"><span data-stu-id="c34de-355">f.</span></span> <span data-ttu-id="c34de-356">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-356">Click **Save**.</span></span> 

3. <span data-ttu-id="c34de-357">En el portal clásico de hello Azure AD, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c34de-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="c34de-358">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="c34de-359">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="c34de-360">![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c34de-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="c34de-361">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="c34de-361">Configuring user provisioning</span></span>
<span data-ttu-id="c34de-362">objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="c34de-363">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c34de-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="c34de-364">En hello Azure clásico portal de administración en hello **ServiceNow** página de integración de aplicaciones, haga clic en **configurar aprovisionamiento de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c34de-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="c34de-365">![Aprovisionamiento de usuarios](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Aprovisionamiento de usuarios")</span><span class="sxs-lookup"><span data-stu-id="c34de-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="c34de-366">En hello **escriba el aprovisionamiento automático de usuarios de ServiceNow credenciales tooenable** , proporcione Hola siguientes opciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="c34de-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="c34de-367">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-367">a.</span></span> <span data-ttu-id="c34de-368">Hola **nombre de la instancia de ServiceNow** cuadro de texto, nombre de la instancia de tipo hello ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="c34de-369">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-369">b.</span></span> <span data-ttu-id="c34de-370">Hola **nombre de usuario de administrador de ServiceNow** cuadro de texto, nombre de tipo hello de hello cuenta de administrador de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="c34de-371">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-371">c.</span></span> <span data-ttu-id="c34de-372">Hola **contraseña de administrador de ServiceNow** cuadro de texto, escriba la contraseña de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="c34de-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="c34de-373">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-373">d.</span></span> <span data-ttu-id="c34de-374">Haga clic en **validar** tooverify su configuración.</span><span class="sxs-lookup"><span data-stu-id="c34de-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="c34de-375">e.</span><span class="sxs-lookup"><span data-stu-id="c34de-375">e.</span></span> <span data-ttu-id="c34de-376">Haga clic en hello **siguiente** Hola de botón tooopen **pasos siguientes** página.</span><span class="sxs-lookup"><span data-stu-id="c34de-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="c34de-377">f.</span><span class="sxs-lookup"><span data-stu-id="c34de-377">f.</span></span> <span data-ttu-id="c34de-378">Si desea que todos los usuarios toothis application tooprovision, seleccione "**aprovisionar automáticamente todas las cuentas de usuario en la aplicación de hello directorio toothis**".</span><span class="sxs-lookup"><span data-stu-id="c34de-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="c34de-379">![Pasos siguientes](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Pasos siguientes")</span><span class="sxs-lookup"><span data-stu-id="c34de-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="c34de-380">g.</span><span class="sxs-lookup"><span data-stu-id="c34de-380">g.</span></span> <span data-ttu-id="c34de-381">En hello **pasos siguientes** página, haga clic en **completar** toosave su configuración.</span><span class="sxs-lookup"><span data-stu-id="c34de-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c34de-382">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c34de-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="c34de-383">En esta sección, creará un usuario de prueba en el portal clásico de hello llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c34de-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="c34de-385">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c34de-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c34de-386">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c34de-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="c34de-388">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="c34de-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="c34de-389">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c34de-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c34de-391">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="c34de-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="c34de-393">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c34de-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="c34de-395">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-395">a.</span></span> <span data-ttu-id="c34de-396">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="c34de-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="c34de-397">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-397">b.</span></span> <span data-ttu-id="c34de-398">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c34de-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="c34de-399">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-399">c.</span></span> <span data-ttu-id="c34de-400">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c34de-400">Click **Next**.</span></span>

6. <span data-ttu-id="c34de-401">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c34de-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="c34de-403">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-403">a.</span></span> <span data-ttu-id="c34de-404">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="c34de-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="c34de-405">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-405">b.</span></span> <span data-ttu-id="c34de-406">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c34de-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="c34de-407">c.</span><span class="sxs-lookup"><span data-stu-id="c34de-407">c.</span></span> <span data-ttu-id="c34de-408">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c34de-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="c34de-409">d.</span><span class="sxs-lookup"><span data-stu-id="c34de-409">d.</span></span> <span data-ttu-id="c34de-410">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="c34de-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="c34de-411">e.</span><span class="sxs-lookup"><span data-stu-id="c34de-411">e.</span></span> <span data-ttu-id="c34de-412">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c34de-412">Click **Next**.</span></span>

7. <span data-ttu-id="c34de-413">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="c34de-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="c34de-415">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c34de-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="c34de-417">a.</span><span class="sxs-lookup"><span data-stu-id="c34de-417">a.</span></span> <span data-ttu-id="c34de-418">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c34de-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="c34de-419">b.</span><span class="sxs-lookup"><span data-stu-id="c34de-419">b.</span></span> <span data-ttu-id="c34de-420">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="c34de-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="c34de-421">Creación de un usuario de prueba de ServiceNow</span><span class="sxs-lookup"><span data-stu-id="c34de-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="c34de-422">En esta sección, creará un usuario llamado Britta Simon en ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="c34de-423">En esta sección, creará un usuario llamado Britta Simon en ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="c34de-424">Si no sabe cómo tooadd un usuario en su ServiceNow o ServiceNow Express cuenta, póngase en contacto con el equipo de soporte técnico de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c34de-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c34de-425">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c34de-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="c34de-426">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooServiceNow de acceso.</span><span class="sxs-lookup"><span data-stu-id="c34de-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c34de-428">**tooassign Britta Simon tooServiceNow, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c34de-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="c34de-429">En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="c34de-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Asignar usuario][201] 

2. <span data-ttu-id="c34de-431">En la lista de aplicaciones de hello, seleccione **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="c34de-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="c34de-433">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c34de-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Asignar usuario][203] 

4. <span data-ttu-id="c34de-435">En la lista de todos los usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c34de-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="c34de-436">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="c34de-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="c34de-438">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c34de-438">Testing single sign-on</span></span>
<span data-ttu-id="c34de-439">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c34de-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c34de-440">Al hacer clic en icono de ServiceNow Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour ServiceNow aplicación.</span><span class="sxs-lookup"><span data-stu-id="c34de-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c34de-441">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c34de-441">Additional resources</span></span>
* [<span data-ttu-id="c34de-442">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c34de-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c34de-443">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c34de-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
