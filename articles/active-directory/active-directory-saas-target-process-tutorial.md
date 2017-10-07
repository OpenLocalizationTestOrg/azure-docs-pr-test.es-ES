---
title: "Tutorial: Integración de Azure Active Directory con TargetProcess | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="a0821-103">Tutorial: Integración de Azure Active Directory con TargetProcess</span><span class="sxs-lookup"><span data-stu-id="a0821-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="a0821-104">En este tutorial, aprenderá cómo toointegrate TargetProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0821-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0821-105">Integración TargetProcess con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a0821-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a0821-106">Puede controlar en Azure AD que tenga acceso tooTargetProcess</span><span class="sxs-lookup"><span data-stu-id="a0821-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="a0821-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTargetProcess (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0821-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0821-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a0821-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a0821-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0821-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0821-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a0821-110">Prerequisites</span></span>

<span data-ttu-id="a0821-111">integración de Azure AD con TargetProcess tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a0821-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="a0821-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0821-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0821-113">Una suscripción habilitada para inicio de sesión único en TargetProcess</span><span class="sxs-lookup"><span data-stu-id="a0821-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0821-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a0821-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0821-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a0821-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0821-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a0821-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0821-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0821-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0821-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a0821-118">Scenario description</span></span>
<span data-ttu-id="a0821-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a0821-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0821-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="a0821-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0821-121">Agregar TargetProcess de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a0821-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="a0821-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0821-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="a0821-123">Agregar TargetProcess de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a0821-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="a0821-124">integración de hello tooconfigure de TargetProcess en Azure AD, deberá tooadd TargetProcess de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a0821-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a0821-125">**tooadd TargetProcess de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0821-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0821-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a0821-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0821-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a0821-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a0821-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a0821-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a0821-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a0821-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a0821-133">En el cuadro de búsqueda de hello, escriba **TargetProcess**, seleccione **TargetProcess** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a0821-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Incorporación de TargetProcess desde la galería](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a0821-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0821-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a0821-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con TargetProcess con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a0821-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a0821-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TargetProcess es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0821-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="a0821-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TargetProcess debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="a0821-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="a0821-139">En TargetProcess, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0821-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a0821-140">tooconfigure y prueba de inicio de sesión único en Azure AD con TargetProcess, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a0821-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a0821-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="a0821-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a0821-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0821-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0821-143">**[Crear un usuario de prueba TargetProcess](#create-a-targetprocess-test-user) ** -toohave un equivalente de Britta Simon en TargetProcess que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="a0821-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0821-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a0821-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0821-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a0821-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a0821-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0821-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a0821-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="a0821-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="a0821-148">**inicio de sesión único en Azure AD tooconfigure con TargetProcess, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0821-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0821-149">En el portal de Azure, en Hola Hola **TargetProcess** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a0821-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a0821-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a0821-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="a0821-153">En hello **TargetProcess dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a0821-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Sección Dominio y direcciones URL de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="a0821-155">a.</span><span class="sxs-lookup"><span data-stu-id="a0821-155">a.</span></span> <span data-ttu-id="a0821-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="a0821-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="a0821-157">b.</span><span class="sxs-lookup"><span data-stu-id="a0821-157">b.</span></span> <span data-ttu-id="a0821-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="a0821-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0821-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="a0821-159">These values are not real.</span></span> <span data-ttu-id="a0821-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="a0821-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a0821-161">Póngase en contacto con [equipo de soporte técnico de cliente de TargetProcess](mailto:support@targetprocess.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="a0821-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="a0821-162">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a0821-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="a0821-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a0821-164">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0821-166">En hello **TargetProcess configuración** sección, haga clic en **configurar TargetProcess** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="a0821-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a0821-167">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="a0821-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sección Configuración de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="a0821-169">Inicio de sesión tooyour TargetProcess aplicación como administrador.</span><span class="sxs-lookup"><span data-stu-id="a0821-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="a0821-170">En el menú de hello en la parte superior de hello, haga clic en **el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="a0821-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Configuración](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="a0821-172">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="a0821-172">Click **Settings**.</span></span>
   
    ![Configuración](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="a0821-174">Haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a0821-174">Click **Single Sign-on**.</span></span>
   
    ![clic en Inicio de sesión único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="a0821-176">En hello inicio de sesión único cuadro de diálogo Configuración, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a0821-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="a0821-178">a.</span><span class="sxs-lookup"><span data-stu-id="a0821-178">a.</span></span> <span data-ttu-id="a0821-179">Haga lic en **Habilitar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a0821-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="a0821-180">b.</span><span class="sxs-lookup"><span data-stu-id="a0821-180">b.</span></span> <span data-ttu-id="a0821-181">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0821-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a0821-182">c.</span><span class="sxs-lookup"><span data-stu-id="a0821-182">c.</span></span> <span data-ttu-id="a0821-183">Abra el certificado descargado en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="a0821-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="a0821-184">d.</span><span class="sxs-lookup"><span data-stu-id="a0821-184">d.</span></span> <span data-ttu-id="a0821-185">Haga clic en **Habilitar aprovisionamiento de JIT**.</span><span class="sxs-lookup"><span data-stu-id="a0821-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="a0821-186">e.</span><span class="sxs-lookup"><span data-stu-id="a0821-186">e.</span></span> <span data-ttu-id="a0821-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a0821-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a0821-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="a0821-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a0821-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="a0821-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a0821-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0821-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a0821-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0821-191">Create an Azure AD test user</span></span>
<span data-ttu-id="a0821-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="a0821-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a0821-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0821-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0821-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a0821-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0821-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a0821-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![lista de hello toodisplay de usuarios](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0821-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0821-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0821-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="a0821-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Sección Usuario](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0821-203">a.</span><span class="sxs-lookup"><span data-stu-id="a0821-203">a.</span></span> <span data-ttu-id="a0821-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0821-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0821-205">b.</span><span class="sxs-lookup"><span data-stu-id="a0821-205">b.</span></span> <span data-ttu-id="a0821-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0821-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0821-207">c.</span><span class="sxs-lookup"><span data-stu-id="a0821-207">c.</span></span> <span data-ttu-id="a0821-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a0821-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a0821-209">d.</span><span class="sxs-lookup"><span data-stu-id="a0821-209">d.</span></span> <span data-ttu-id="a0821-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a0821-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="a0821-211">Creación de un usuario de prueba de TargetProcess</span><span class="sxs-lookup"><span data-stu-id="a0821-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="a0821-212">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en TargetProcess toocreate.</span><span class="sxs-lookup"><span data-stu-id="a0821-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="a0821-213">TargetProcess admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="a0821-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="a0821-214">Ya lo ha habilitado en [Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a0821-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="a0821-215">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="a0821-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a0821-216">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0821-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a0821-217">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTargetProcess.</span><span class="sxs-lookup"><span data-stu-id="a0821-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a0821-219">**tooassign Britta Simon tooTargetProcess, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0821-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0821-220">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a0821-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a0821-222">En la lista de aplicaciones de hello, seleccione **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="a0821-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess en la lista de aplicaciones](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="a0821-224">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a0821-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a0821-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a0821-226">Click **Add** button.</span></span> <span data-ttu-id="a0821-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a0821-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a0821-229">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0821-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a0821-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a0821-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0821-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a0821-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a0821-232">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a0821-232">Test single sign-on</span></span>

<span data-ttu-id="a0821-233">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a0821-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a0821-234">Al hacer clic en hello TargetProcess disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour TargetProcess aplicación.</span><span class="sxs-lookup"><span data-stu-id="a0821-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="a0821-235">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a0821-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0821-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a0821-236">Additional resources</span></span>

* [<span data-ttu-id="a0821-237">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0821-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0821-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a0821-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

