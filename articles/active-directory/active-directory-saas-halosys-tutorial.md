---
title: "Tutorial: Integración de Azure Active Directory con Halosys | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Halosys con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="cc701-103">Tutorial: Integración de Azure Active Directory con Halosys</span><span class="sxs-lookup"><span data-stu-id="cc701-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="cc701-104">En este tutorial, aprenderá cómo toointegrate Halosys con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc701-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc701-105">Integración Halosys con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cc701-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc701-106">Puede controlar en Azure AD que tenga acceso tooHalosys</span><span class="sxs-lookup"><span data-stu-id="cc701-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="cc701-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHalosys (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc701-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc701-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="cc701-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="cc701-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc701-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc701-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cc701-110">Prerequisites</span></span>

<span data-ttu-id="cc701-111">integración de Azure AD con Halosys tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cc701-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="cc701-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc701-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc701-113">Una suscripción habilitada para el inicio de sesión único en Halosys.</span><span class="sxs-lookup"><span data-stu-id="cc701-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="cc701-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cc701-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="cc701-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cc701-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc701-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cc701-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cc701-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc701-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="cc701-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cc701-118">Scenario description</span></span>
<span data-ttu-id="cc701-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cc701-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="cc701-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cc701-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc701-121">Agregar Halosys desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc701-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="cc701-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc701-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="cc701-123">Agregar Halosys desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc701-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="cc701-124">integración de hello tooconfigure de Halosys en Azure AD, deberá tooadd Halosys de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cc701-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc701-125">**tooadd Halosys de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc701-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc701-126">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc701-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="cc701-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="cc701-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="cc701-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="cc701-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplicaciones][2]

4. <span data-ttu-id="cc701-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="cc701-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplicaciones][3]

5. <span data-ttu-id="cc701-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="cc701-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Aplicaciones][4]

6. <span data-ttu-id="cc701-135">En el cuadro de búsqueda de hello, escriba **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="cc701-135">In hello search box, type **Halosys**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="cc701-137">En el panel de resultados de hello, seleccione **Halosys**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc701-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc701-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc701-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc701-140">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Halosys con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc701-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc701-141">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Halosys es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc701-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="cc701-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Halosys debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cc701-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="cc701-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Halosys.</span><span class="sxs-lookup"><span data-stu-id="cc701-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="cc701-144">tooconfigure y prueba de inicio de sesión único en Azure AD con Halosys, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cc701-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc701-145">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cc701-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc701-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc701-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc701-147">**[Crear un usuario de prueba Halosys](#creating-a-halosys-test-user)**  -toohave un equivalente de Britta Simon en Halosys que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="cc701-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cc701-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cc701-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc701-149">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cc701-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc701-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc701-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc701-151">En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación Halosys.</span><span class="sxs-lookup"><span data-stu-id="cc701-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="cc701-152">**inicio de sesión único en Azure AD tooconfigure con Halosys, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc701-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc701-153">En portal clásico de hello, en hello **Halosys** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cc701-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar inicio de sesión único][6] 

2. <span data-ttu-id="cc701-155">En hello **¿cómo desea que los usuarios toosign en tooHalosys** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cc701-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="cc701-157">En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cc701-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="cc701-159">a.</span><span class="sxs-lookup"><span data-stu-id="cc701-159">a.</span></span> <span data-ttu-id="cc701-160">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por la aplicación de Halosys de tooyour toosign en los usuarios con hello sigue el patrón: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="cc701-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="cc701-161">Hola b.In **dirección URL de identificación** cuadro de texto, escriba la dirección URL Hola Hola siguiente patrón: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="cc701-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="cc701-162">En hello **configurar inicio de sesión único en Halosys** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo:</span><span class="sxs-lookup"><span data-stu-id="cc701-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="cc701-164">tooget SSO configurado para la aplicación, póngase en contacto con el equipo de soporte técnico de Halosys y proporcionarles siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="cc701-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="cc701-165">Hola • descargado **archivo de metadatos**</span><span class="sxs-lookup"><span data-stu-id="cc701-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="cc701-166">• hello **dirección URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="cc701-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="cc701-167">En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cc701-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Inicio de sesión único de Azure AD ][10]

7. <span data-ttu-id="cc701-169">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="cc701-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Inicio de sesión único de Azure AD ][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc701-171">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc701-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc701-172">En esta sección, creará un usuario de prueba en el portal clásico de hello llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc701-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Creación de un usuario de Azure AD][20]

<span data-ttu-id="cc701-174">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc701-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc701-175">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc701-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="cc701-177">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="cc701-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="cc701-178">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cc701-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc701-180">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="cc701-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="cc701-182">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello: ![crear un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="cc701-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="cc701-183">a.</span><span class="sxs-lookup"><span data-stu-id="cc701-183">a.</span></span> <span data-ttu-id="cc701-184">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="cc701-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="cc701-185">b.</span><span class="sxs-lookup"><span data-stu-id="cc701-185">b.</span></span> <span data-ttu-id="cc701-186">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc701-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc701-187">c.</span><span class="sxs-lookup"><span data-stu-id="cc701-187">c.</span></span> <span data-ttu-id="cc701-188">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cc701-188">Click **Next**.</span></span>

6.  <span data-ttu-id="cc701-189">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello: ![crear un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="cc701-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="cc701-190">a.</span><span class="sxs-lookup"><span data-stu-id="cc701-190">a.</span></span> <span data-ttu-id="cc701-191">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="cc701-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="cc701-192">b.</span><span class="sxs-lookup"><span data-stu-id="cc701-192">b.</span></span> <span data-ttu-id="cc701-193">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cc701-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="cc701-194">c.</span><span class="sxs-lookup"><span data-stu-id="cc701-194">c.</span></span> <span data-ttu-id="cc701-195">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cc701-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="cc701-196">d.</span><span class="sxs-lookup"><span data-stu-id="cc701-196">d.</span></span> <span data-ttu-id="cc701-197">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="cc701-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="cc701-198">e.</span><span class="sxs-lookup"><span data-stu-id="cc701-198">e.</span></span> <span data-ttu-id="cc701-199">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cc701-199">Click **Next**.</span></span>

7. <span data-ttu-id="cc701-200">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="cc701-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="cc701-202">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cc701-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="cc701-204">a.</span><span class="sxs-lookup"><span data-stu-id="cc701-204">a.</span></span> <span data-ttu-id="cc701-205">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cc701-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="cc701-206">b.</span><span class="sxs-lookup"><span data-stu-id="cc701-206">b.</span></span> <span data-ttu-id="cc701-207">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="cc701-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="cc701-208">Creación de un usuario de prueba de Halosys</span><span class="sxs-lookup"><span data-stu-id="cc701-208">Creating a Halosys test user</span></span>

<span data-ttu-id="cc701-209">En esta sección, creará un usuario llamado Britta Simon en Halosys.</span><span class="sxs-lookup"><span data-stu-id="cc701-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="cc701-210">Trabaje con Halosys usuarios de soporte técnico team tooadd hello en la plataforma de Halosys Hola.</span><span class="sxs-lookup"><span data-stu-id="cc701-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc701-211">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc701-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc701-212">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooHalosys de acceso.</span><span class="sxs-lookup"><span data-stu-id="cc701-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cc701-214">**tooassign Britta Simon tooHalosys, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc701-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc701-215">En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="cc701-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cc701-217">En la lista de aplicaciones de hello, seleccione **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="cc701-217">In hello applications list, select **Halosys**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="cc701-219">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cc701-219">In hello menu on hello top, click **Users**.</span></span>

    ![Asignar usuario][203]

4. <span data-ttu-id="cc701-221">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cc701-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="cc701-222">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="cc701-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Asignar usuario][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="cc701-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cc701-224">Testing single sign-on</span></span>

<span data-ttu-id="cc701-225">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cc701-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc701-226">Al hacer clic en hello Halosys el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Halosys aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc701-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cc701-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cc701-227">Additional resources</span></span>

* [<span data-ttu-id="cc701-228">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc701-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc701-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc701-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
