---
title: "Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Splunk Enterprise y Splunk en la nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="1e621-103">Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="1e621-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="1e621-104">En este tutorial, aprenderá cómo toointegrate Splunk Enterprise y Splunk en la nube con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e621-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e621-105">Integración de Splunk Enterprise y Splunk en la nube con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1e621-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e621-106">Puede controlar en Azure AD que tenga acceso tooSplunk Enterprise y Splunk en la nube</span><span class="sxs-lookup"><span data-stu-id="1e621-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="1e621-107">Puede habilitar la get ha iniciado sesión tooSplunk de usuarios tooautomatically grandes empresas y nube Splunk inicio de sesión único (SSO) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e621-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e621-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="1e621-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="1e621-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e621-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e621-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e621-110">Prerequisites</span></span>

<span data-ttu-id="1e621-111">tooconfigure integración de Azure AD con Splunk Enterprise y Splunk en la nube, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1e621-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="1e621-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e621-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e621-113">Una suscripción habilitada para el SSO en Splunk Enterprise o Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="1e621-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="1e621-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1e621-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="1e621-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1e621-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e621-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1e621-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1e621-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e621-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1e621-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1e621-118">Scenario description</span></span>
<span data-ttu-id="1e621-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1e621-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1e621-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="1e621-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e621-121">Agregar Splunk Enterprise y Splunk en la nube de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1e621-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="1e621-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e621-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="1e621-123">Agregar Splunk empresarial y en la nube Splunk de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1e621-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="1e621-124">integración de hello tooconfigure de empresa de Splunk y Splunk en la nube en Azure AD, necesita tooadd Splunk Enterprise y Splunk en la nube de lista de tooyour Hola Galería de las aplicaciones de SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1e621-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e621-125">**tooadd Splunk Enterprise y Splunk en la nube de la Galería de hello, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1e621-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e621-126">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e621-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="1e621-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="1e621-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="1e621-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="1e621-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplicaciones][2]

4. <span data-ttu-id="1e621-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="1e621-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplicaciones][3]

5. <span data-ttu-id="1e621-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="1e621-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Aplicaciones][4]

6. <span data-ttu-id="1e621-135">En el cuadro de búsqueda de hello, escriba **Splunk Enterprise o nube Splunk**.</span><span class="sxs-lookup"><span data-stu-id="1e621-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="1e621-137">En el panel de resultados de hello, seleccione **Splunk empresarial y en la nube Splunk**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1e621-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1e621-139">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e621-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1e621-140">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Splunk Enterprise y Splunk Cloud mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1e621-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e621-141">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Splunk Enterprise y Splunk en la nube es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e621-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="1e621-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Splunk Enterprise y Splunk en la nube debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="1e621-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="1e621-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Splunk Enterprise y Splunk en la nube.</span><span class="sxs-lookup"><span data-stu-id="1e621-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="1e621-144">tooconfigure y prueba de inicio de sesión único en Azure AD con Splunk Enterprise y Splunk en la nube, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1e621-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e621-145">**[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="1e621-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e621-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e621-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e621-147">**[Crear un usuario de prueba Splunk empresarial y en la nube Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user) ** -toohave un equivalente de Britta Simon de empresa de Splunk y Splunk en la nube que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="1e621-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1e621-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1e621-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e621-149">**[Probar el inicio de sesión único](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1e621-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1e621-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e621-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1e621-151">En esta sección, se habilita el SSO de Azure AD en el portal clásico de Hola y configura SSO en la aplicación empresarial de Splunk y Splunk en la nube.</span><span class="sxs-lookup"><span data-stu-id="1e621-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="1e621-152">**tooconfigure inicio de sesión único en Azure AD con Splunk Enterprise y Splunk en la nube, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1e621-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e621-153">En portal clásico de hello, en hello **Splunk empresarial y en la nube Splunk** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1e621-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar inicio de sesión único][6] 

2. <span data-ttu-id="1e621-155">En hello **cómo le gustaría toosign a los usuarios en tooSplunk empresarial y en la nube Splunk** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e621-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="1e621-157">En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1e621-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="1e621-159">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada los usuarios toosign en tooyour Splunk Enterprise y aplicación de nube de Splunk mediante Hola sigue el patrón:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="1e621-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="1e621-160">Hola **identificador** cuadro de texto, escriba Hola la dirección URL del servidor Splunk.</span><span class="sxs-lookup"><span data-stu-id="1e621-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="1e621-161">Hola **dirección URL de respuesta** cuadro de texto, escriba la dirección URL Hola con hello sigue el patrón:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="1e621-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="1e621-162">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e621-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="1e621-163">En hello **configurar inicio de sesión único en Splunk empresarial y en la nube Splunk** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1e621-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="1e621-165">Haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1e621-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="1e621-166">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e621-166">Click **Next**.</span></span>

5. <span data-ttu-id="1e621-167">tooget SSO configurado para la aplicación, póngase en contacto con Splunk empresarial y el equipo de soporte técnico de Splunk en la nube y proporcionarles siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="1e621-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="1e621-168">Hola descargado **federaton metadatos**</span><span class="sxs-lookup"><span data-stu-id="1e621-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="1e621-169">En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e621-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Inicio de sesión único de Azure AD ][10]

7. <span data-ttu-id="1e621-171">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="1e621-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1e621-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e621-173">Create an Azure AD test user</span></span>
<span data-ttu-id="1e621-174">En esta sección, creará un usuario de prueba en el portal clásico de hello llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e621-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="1e621-176">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1e621-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e621-177">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e621-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1e621-179">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="1e621-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="1e621-180">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1e621-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e621-182">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="1e621-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1e621-184">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1e621-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="1e621-186">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="1e621-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="1e621-187">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e621-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="1e621-188">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e621-188">Click **Next**.</span></span>

6.  <span data-ttu-id="1e621-189">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1e621-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="1e621-191">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="1e621-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="1e621-192">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e621-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="1e621-193">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e621-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="1e621-194">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="1e621-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="1e621-195">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e621-195">Click **Next**.</span></span>

7. <span data-ttu-id="1e621-196">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="1e621-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1e621-198">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1e621-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="1e621-200">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1e621-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="1e621-201">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="1e621-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="1e621-202">Creación de un usuario de prueba de Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="1e621-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="1e621-203">En esta sección, creará un usuario llamado Britta Simon en Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="1e621-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="1e621-204">Trabaje con Splunk empresarial y en la nube Splunk usuarios de soporte técnico team tooadd hello en hello Splunk Enterprise y plataforma de nube Splunk.</span><span class="sxs-lookup"><span data-stu-id="1e621-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1e621-205">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e621-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1e621-206">En esta sección, se habilita Britta Simon toouse SSOy Azure conceder su acceso tooSplunk Enterprise y Splunk en la nube.</span><span class="sxs-lookup"><span data-stu-id="1e621-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1e621-208">**tooassign Britta Simon tooSplunk Enterprise y Splunk en la nube, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1e621-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e621-209">En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="1e621-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1e621-211">En la lista de aplicaciones de hello, seleccione **Splunk empresarial y en la nube Splunk**.</span><span class="sxs-lookup"><span data-stu-id="1e621-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="1e621-213">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1e621-213">In hello menu on hello top, click **Users**.</span></span>

    ![Asignar usuario][203]

4. <span data-ttu-id="1e621-215">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e621-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="1e621-216">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="1e621-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1e621-218">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1e621-218">Test single sign-on</span></span>

<span data-ttu-id="1e621-219">En esta sección, probará la AD SSOonfiguration de Azure con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1e621-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="1e621-220">Al hacer clic en hello Splunk empresarial y el icono de nube Splunk Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación empresarial de Splunk y Splunk en la nube.</span><span class="sxs-lookup"><span data-stu-id="1e621-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1e621-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1e621-221">Additional resources</span></span>

* [<span data-ttu-id="1e621-222">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e621-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e621-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e621-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
