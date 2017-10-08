---
title: "Tutorial: Integración de Azure Active Directory con @Task| Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="2b301-103">Tutorial: integración de Azure Active Directory con @Task</span><span class="sxs-lookup"><span data-stu-id="2b301-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="2b301-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate @Task con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b301-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="2b301-105">Integrar @Task con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2b301-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="2b301-106">Puede controlar en Azure AD que tenga accesotoo@Task</span><span class="sxs-lookup"><span data-stu-id="2b301-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="2b301-107">Se pueden permitir a los usuarios obtener tooautomatically ha iniciado sesión too@Task (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b301-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="2b301-108">Puede administrar las cuentas en una ubicación central: Hola Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="2b301-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="2b301-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b301-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b301-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2b301-110">Prerequisites</span></span>
<span data-ttu-id="2b301-111">integración de Azure AD tooconfigure con @Task, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2b301-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="2b301-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b301-112">An Azure AD subscription</span></span>
* <span data-ttu-id="2b301-113">Una suscripción habilitada para inicio de sesión único en @Task</span><span class="sxs-lookup"><span data-stu-id="2b301-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b301-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2b301-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="2b301-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2b301-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="2b301-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2b301-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="2b301-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b301-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="2b301-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2b301-118">Scenario Description</span></span>
<span data-ttu-id="2b301-119">objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2b301-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="2b301-120">escenario de Hello descrito en este tutorial consta de tres pilares principales:</span><span class="sxs-lookup"><span data-stu-id="2b301-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="2b301-121">Agregar @Task de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2b301-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="2b301-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b301-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="2b301-123">Agregar @Task de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2b301-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="2b301-124">integración de hello tooconfigure de @Task en Azure AD, necesita tooadd @Task de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2b301-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b301-125">**tooadd @Task desde la Galería de hello, llevar a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b301-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b301-126">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b301-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="2b301-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="2b301-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="2b301-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="2b301-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicaciones][2] 
4. <span data-ttu-id="2b301-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="2b301-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3] 
5. <span data-ttu-id="2b301-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="2b301-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicaciones][4] 
6. <span data-ttu-id="2b301-135">En el cuadro de búsqueda de hello, escriba  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="2b301-135">In hello search box, type **@Task**.</span></span>
   
    ![Aplicaciones][5] 
7. <span data-ttu-id="2b301-137">En el panel de resultados de hello, seleccione  **@Task** y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b301-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplicaciones][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b301-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b301-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b301-140">Hola objetivo de esta sección es tooshow, cómo tooconfigure y prueba de Azure AD único inicio de sesión con @Task en función de un usuario de prueba denominado "Bárbara Simon".</span><span class="sxs-lookup"><span data-stu-id="2b301-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b301-141">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en @Task tooan usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b301-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="2b301-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en @Task necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="2b301-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="2b301-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en @Task.</span><span class="sxs-lookup"><span data-stu-id="2b301-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="2b301-144">prueba Azure AD y tooconfigure inicio de sesión único con @Task, necesita hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2b301-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b301-145">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="2b301-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b301-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b301-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b301-147">**[Crear un @Tasktest usuario](#creating-a-halogen-software-test-user)**  -toohave un equivalente de Britta Simon en @Taskthat es representación toohello vinculado Azure AD de ella.</span><span class="sxs-lookup"><span data-stu-id="2b301-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2b301-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2b301-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b301-149">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2b301-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b301-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b301-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="2b301-151">objetivo de Hola de esta sección es tooenable Azure AD single sign-on en hello portal de Azure clásico y tooconfigure inicio de sesión único en su @Task aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b301-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="2b301-152">**tooconfigure inicio de sesión único en Azure AD con @Task, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b301-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b301-153">En el portal de Azure clásico en Hola Hola  **@Task**  página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2b301-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][6] 
2. <span data-ttu-id="2b301-155">En hello **¿cómo desea que los usuarios toosign en too@Task**  página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b301-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][7] 
3. <span data-ttu-id="2b301-157">En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2b301-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configurar las opciones de la aplicación][8] 
   
     <span data-ttu-id="2b301-159">a.</span><span class="sxs-lookup"><span data-stu-id="2b301-159">a.</span></span> <span data-ttu-id="2b301-160">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por los usuarios en toosign tooyour @Task aplicación (p. ej.:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="2b301-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="2b301-161">b.</span><span class="sxs-lookup"><span data-stu-id="2b301-161">b.</span></span> <span data-ttu-id="2b301-162">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b301-162">Click **Next**.</span></span>
4. <span data-ttu-id="2b301-163">En hello **configurar inicio de sesión único en @Task**  página, haga clic en **descargar metadatos**, guarde el archivo de metadatos de hello localmente en el equipo y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b301-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Qué es Azure AD Connect][9] 
5. <span data-ttu-id="2b301-165">Inicio de sesión tooyour @Task como administrador.</span><span class="sxs-lookup"><span data-stu-id="2b301-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="2b301-166">Vaya demasiado**inicio de sesión único en la configuración**.</span><span class="sxs-lookup"><span data-stu-id="2b301-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="2b301-167">En hello **Single Sign-On** cuadro de diálogo, realizar pasos de Hola</span><span class="sxs-lookup"><span data-stu-id="2b301-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Configurar inicio de sesión único][23]
   
    <span data-ttu-id="2b301-169">a.</span><span class="sxs-lookup"><span data-stu-id="2b301-169">a.</span></span> <span data-ttu-id="2b301-170">En **Tipo**, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="2b301-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="2b301-171">b.</span><span class="sxs-lookup"><span data-stu-id="2b301-171">b.</span></span> <span data-ttu-id="2b301-172">Seleccione **Service Provider ID** (Id. del proveedor de servicios).</span><span class="sxs-lookup"><span data-stu-id="2b301-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="2b301-173">c.</span><span class="sxs-lookup"><span data-stu-id="2b301-173">c.</span></span> <span data-ttu-id="2b301-174">En el portal de Azure clásico hello, copie hello **dirección URL de inicio de sesión remoto**y, a continuación, péguelo en hello **dirección URL del Portal de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2b301-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="2b301-175">d.</span><span class="sxs-lookup"><span data-stu-id="2b301-175">d.</span></span> <span data-ttu-id="2b301-176">En el portal de Azure clásico hello, copie Hola **dirección URL del servicio de cierre de sesión único**y, a continuación, péguelo en hello **dirección URL de cierre de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2b301-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="2b301-177">e.</span><span class="sxs-lookup"><span data-stu-id="2b301-177">e.</span></span> <span data-ttu-id="2b301-178">En el portal de Azure clásico hello, copie hello **cambiar dirección URL de contraseña**y, a continuación, péguelo en hello **cambiar dirección URL de contraseña** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2b301-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="2b301-179">f.</span><span class="sxs-lookup"><span data-stu-id="2b301-179">f.</span></span> <span data-ttu-id="2b301-180">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2b301-180">Click **Save**.</span></span>
8. <span data-ttu-id="2b301-181">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b301-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Qué es Azure AD Connect][10]
9. <span data-ttu-id="2b301-183">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="2b301-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Qué es Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b301-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b301-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b301-186">objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2b301-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="2b301-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b301-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b301-189">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b301-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="2b301-191">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="2b301-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="2b301-192">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2b301-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="2b301-194">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="2b301-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="2b301-196">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2b301-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="2b301-198">a.</span><span class="sxs-lookup"><span data-stu-id="2b301-198">a.</span></span> <span data-ttu-id="2b301-199">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="2b301-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="2b301-200">b.</span><span class="sxs-lookup"><span data-stu-id="2b301-200">b.</span></span> <span data-ttu-id="2b301-201">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b301-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="2b301-202">c.</span><span class="sxs-lookup"><span data-stu-id="2b301-202">c.</span></span> <span data-ttu-id="2b301-203">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b301-203">Click **Next**.</span></span>
6. <span data-ttu-id="2b301-204">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2b301-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="2b301-206">a.</span><span class="sxs-lookup"><span data-stu-id="2b301-206">a.</span></span> <span data-ttu-id="2b301-207">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="2b301-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="2b301-208">b.</span><span class="sxs-lookup"><span data-stu-id="2b301-208">b.</span></span> <span data-ttu-id="2b301-209">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2b301-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="2b301-210">c.</span><span class="sxs-lookup"><span data-stu-id="2b301-210">c.</span></span> <span data-ttu-id="2b301-211">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2b301-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="2b301-212">d.</span><span class="sxs-lookup"><span data-stu-id="2b301-212">d.</span></span> <span data-ttu-id="2b301-213">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="2b301-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="2b301-214">e.</span><span class="sxs-lookup"><span data-stu-id="2b301-214">e.</span></span> <span data-ttu-id="2b301-215">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b301-215">Click **Next**.</span></span>

7. <span data-ttu-id="2b301-216">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="2b301-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="2b301-218">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2b301-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="2b301-220">a.</span><span class="sxs-lookup"><span data-stu-id="2b301-220">a.</span></span> <span data-ttu-id="2b301-221">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2b301-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="2b301-222">b.</span><span class="sxs-lookup"><span data-stu-id="2b301-222">b.</span></span> <span data-ttu-id="2b301-223">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="2b301-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="2b301-224">Creación de un usuario de prueba de @Task</span><span class="sxs-lookup"><span data-stu-id="2b301-224">Creating an @Task test user</span></span>
<span data-ttu-id="2b301-225">objetivo de Hola de esta sección es un usuario llamado Britta Simon toocreate @Task.</span><span class="sxs-lookup"><span data-stu-id="2b301-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="2b301-226">**un usuario llamado Britta Simon toocreate @Task, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b301-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b301-227">Inicio de sesión tooyour @Task como administrador.</span><span class="sxs-lookup"><span data-stu-id="2b301-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="2b301-228">En el menú de hello en la parte superior de hello, haga clic en **personas**.</span><span class="sxs-lookup"><span data-stu-id="2b301-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="2b301-229">Haga clic en **New Person**(Nueva persona).</span><span class="sxs-lookup"><span data-stu-id="2b301-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="2b301-230">En el cuadro de diálogo de hello nueva persona, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2b301-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de @Task][21] 
   
    <span data-ttu-id="2b301-232">a.</span><span class="sxs-lookup"><span data-stu-id="2b301-232">a.</span></span> <span data-ttu-id="2b301-233">Hola **nombre** cuadro de texto, escriba "Bárbara".</span><span class="sxs-lookup"><span data-stu-id="2b301-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="2b301-234">b.</span><span class="sxs-lookup"><span data-stu-id="2b301-234">b.</span></span> <span data-ttu-id="2b301-235">Hola **Last Name** cuadro de texto, escriba "Simon".</span><span class="sxs-lookup"><span data-stu-id="2b301-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="2b301-236">c.</span><span class="sxs-lookup"><span data-stu-id="2b301-236">c.</span></span> <span data-ttu-id="2b301-237">Hola **dirección de correo electrónico** cuadro de texto, escriba la dirección de correo electrónico Britta Simon en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b301-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="2b301-238">d.</span><span class="sxs-lookup"><span data-stu-id="2b301-238">d.</span></span> <span data-ttu-id="2b301-239">Haga clic en **Add Person**(Agregar persona).</span><span class="sxs-lookup"><span data-stu-id="2b301-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2b301-240">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b301-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="2b301-241">objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su acceso too@Task.</span><span class="sxs-lookup"><span data-stu-id="2b301-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2b301-243">**tooassign Britta Simon too@Task, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b301-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b301-244">En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="2b301-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Asignar usuario][201] 
2. <span data-ttu-id="2b301-246">En la lista de aplicaciones de hello, seleccione  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="2b301-246">In hello applications list, select **@Task**.</span></span>
   
    ![Asignar usuario][202] 
3. <span data-ttu-id="2b301-248">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2b301-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Asignar usuario][203] 
4. <span data-ttu-id="2b301-250">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2b301-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="2b301-251">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="2b301-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="2b301-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2b301-253">Testing Single Sign-On</span></span>
<span data-ttu-id="2b301-254">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2b301-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="2b301-255">Al hacer clic en hello @Task Hola de mosaico en el Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour @Task aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b301-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b301-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2b301-256">Additional Resources</span></span>
* [<span data-ttu-id="2b301-257">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b301-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b301-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b301-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






