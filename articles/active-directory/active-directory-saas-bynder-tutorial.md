---
title: "Tutorial: Integración de Azure Active Directory con Bynder | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="77d28-103">Tutorial: Integración de Azure Active Directory con Bynder</span><span class="sxs-lookup"><span data-stu-id="77d28-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="77d28-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate Bynder con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77d28-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77d28-105">Integración Bynder con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="77d28-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="77d28-106">Puede controlar en Azure AD que tenga acceso tooBynder</span><span class="sxs-lookup"><span data-stu-id="77d28-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="77d28-107">Puede habilitar los usuarios tooautomatically get tooBynder ha iniciado sesión con inicio de sesión único (SSO) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d28-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="77d28-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="77d28-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="77d28-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77d28-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77d28-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="77d28-110">Prerequisites</span></span>
<span data-ttu-id="77d28-111">integración de Azure AD con Bynder tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="77d28-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="77d28-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d28-112">An Azure AD subscription</span></span>
* <span data-ttu-id="77d28-113">Una suscripción habilitada para el inicio de sesión único en Bynder</span><span class="sxs-lookup"><span data-stu-id="77d28-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="77d28-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="77d28-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="77d28-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="77d28-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="77d28-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="77d28-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="77d28-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77d28-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77d28-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="77d28-118">Scenario description</span></span>
<span data-ttu-id="77d28-119">objetivo de Hola de este tutorial es tooenable tootest Microsoft Azure AD SSO en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="77d28-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="77d28-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="77d28-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77d28-121">Agregar Bynder desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="77d28-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="77d28-122">Configuración y prueba del inicio de sesión único de Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d28-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="77d28-123">Agregar Bynder de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="77d28-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="77d28-124">integración de hello tooconfigure de Bynder en Azure AD, deberá tooadd Bynder de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="77d28-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77d28-125">**tooadd Bynder de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77d28-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77d28-126">Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="77d28-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="77d28-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="77d28-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="77d28-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="77d28-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicaciones][2]
4. <span data-ttu-id="77d28-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="77d28-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="77d28-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="77d28-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicaciones][4]
6. <span data-ttu-id="77d28-135">En el cuadro de búsqueda de hello, escriba **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="77d28-135">In hello search box, type **Bynder**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="77d28-137">En el panel de resultados de hello, seleccione **Bynder**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="77d28-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Seleccionar aplicación hello en la Galería de Hola](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="77d28-139">Configuración y prueba del inicio de sesión único de Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d28-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="77d28-140">objetivo de Hola de esta sección es tooshow cómo tooconfigure y probar Microsoft Azure AD SSO con Bynder a partir de un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="77d28-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77d28-141">Para toowork SSO, Azure AD necesita tooknow es qué usuario equivalente de hello en Bynder tooan usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77d28-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="77d28-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Bynder debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="77d28-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="77d28-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Bynder.</span><span class="sxs-lookup"><span data-stu-id="77d28-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="77d28-144">tooconfigure y prueba de Microsoft Azure AD SSO con Bynder, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="77d28-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77d28-145">**[Configuración del inicio de sesión único en Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="77d28-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77d28-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77d28-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="77d28-147">**[Crear un usuario de prueba Bynder](#creating-a-bynder-test-user)**  -toohave un equivalente de Britta Simon en Bynder que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="77d28-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="77d28-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="77d28-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="77d28-149">**[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="77d28-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="77d28-150">Configuración del inicio de sesión único de Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d28-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="77d28-151">En esta sección, habilita el SSO de Microsoft Azure AD en el portal clásico de Hola y configurar SSO en la aplicación Bynder.</span><span class="sxs-lookup"><span data-stu-id="77d28-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="77d28-152">**tooconfigure Microsoft Azure AD SSO con Bynder, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77d28-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="77d28-153">En portal clásico de hello, en hello **Bynder** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77d28-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][6] 
2. <span data-ttu-id="77d28-155">En hello **¿cómo desea que los usuarios toosign en tooBynder** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="77d28-157">En hello **configurar opciones de aplicación** página de diálogo, si lo desea tooconfigure aplicación de hello en **modo iniciado por IDP**, realizar pasos de Hola y haga clic en **siguiente**:</span><span class="sxs-lookup"><span data-stu-id="77d28-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="77d28-159">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="77d28-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="77d28-160">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-160">Click **Next**.</span></span>
4. <span data-ttu-id="77d28-161">Si desea que aplicación de hello tooconfigure en **modo iniciado en SP** en hello **configurar opciones de aplicación** página de diálogo y, a continuación, haga clic en hello **"Show advanced configuración (opcional)"**y, a continuación, escriba Hola **dirección URL de inicio de sesión** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="77d28-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="77d28-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="77d28-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="77d28-165">valor Hola Hola dirección URL de inicio de sesión en este tutorial es simplemente un placeholfer.</span><span class="sxs-lookup"><span data-stu-id="77d28-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="77d28-166">valor real de hello tooget para su entorno, póngase en contacto con Bynder.</span><span class="sxs-lookup"><span data-stu-id="77d28-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="77d28-167">En hello **configurar inicio de sesión único en Bynder** página, realizar pasos de Hola y haga clic en **siguiente**:</span><span class="sxs-lookup"><span data-stu-id="77d28-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="77d28-169">Haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="77d28-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="77d28-170">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-170">Click **Next**.</span></span>
6. <span data-ttu-id="77d28-171">tooget SSO configurado para la aplicación, póngase en contacto con el equipo de soporte de Bynder.</span><span class="sxs-lookup"><span data-stu-id="77d28-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="77d28-172">Adjuntar el archivo de metadatos descargado de Hola y compartirlo con Bynder equipo tooset seguridad SSO en uno de su lados.</span><span class="sxs-lookup"><span data-stu-id="77d28-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="77d28-173">En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][10]
8. <span data-ttu-id="77d28-175">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="77d28-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="77d28-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d28-177">Create an Azure AD test user</span></span>
<span data-ttu-id="77d28-178">objetivo de Hola de esta sección es toocreate un usuario de prueba en el portal clásico de hello llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77d28-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="77d28-180">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77d28-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77d28-181">Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="77d28-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="77d28-183">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="77d28-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="77d28-184">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="77d28-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="77d28-186">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="77d28-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="77d28-188">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="77d28-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="77d28-190">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="77d28-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="77d28-191">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77d28-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="77d28-192">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-192">Click **Next**.</span></span>
6. <span data-ttu-id="77d28-193">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="77d28-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="77d28-195">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="77d28-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="77d28-196">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="77d28-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="77d28-197">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="77d28-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="77d28-198">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="77d28-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="77d28-199">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="77d28-199">Click **Next**.</span></span>
7. <span data-ttu-id="77d28-200">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="77d28-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="77d28-202">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="77d28-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="77d28-204">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="77d28-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="77d28-205">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="77d28-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="77d28-206">Creación de un usuario de prueba de Bynder</span><span class="sxs-lookup"><span data-stu-id="77d28-206">Create a Bynder test user</span></span>
<span data-ttu-id="77d28-207">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Bynder toocreate.</span><span class="sxs-lookup"><span data-stu-id="77d28-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="77d28-208">Bynder admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="77d28-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="77d28-209">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="77d28-209">There is no action item for you in this section.</span></span> <span data-ttu-id="77d28-210">Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento Bynder.</span><span class="sxs-lookup"><span data-stu-id="77d28-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="77d28-211">Si necesita un usuario toocreate manualmente, debe equipo de soporte técnico de toocontact hello Bynder.</span><span class="sxs-lookup"><span data-stu-id="77d28-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="77d28-212">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d28-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="77d28-213">objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure SSO mediante la concesión de su tooBynder de acceso.</span><span class="sxs-lookup"><span data-stu-id="77d28-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Asignar usuario][200]

<span data-ttu-id="77d28-215">**tooassign Britta Simon tooBynder, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77d28-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="77d28-216">En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="77d28-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Asignar usuario][201]
2. <span data-ttu-id="77d28-218">En la lista de aplicaciones de hello, seleccione **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="77d28-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="77d28-220">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="77d28-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Asignar usuario][203]
4. <span data-ttu-id="77d28-222">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="77d28-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="77d28-223">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="77d28-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="77d28-225">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="77d28-225">Test single sign-on</span></span>
<span data-ttu-id="77d28-226">objetivo de Hola de esta sección es tootest la configuración de SSO de Microsoft Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="77d28-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="77d28-227">Al hacer clic en icono de Bynder Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Bynder aplicación.</span><span class="sxs-lookup"><span data-stu-id="77d28-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77d28-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="77d28-228">Additional resources</span></span>
* [<span data-ttu-id="77d28-229">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77d28-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77d28-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77d28-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
