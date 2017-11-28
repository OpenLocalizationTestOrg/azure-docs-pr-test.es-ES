---
title: "Tutorial: Integración de Azure Active Directory con SciQuest Spend Director | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SciQuest dedicar Director."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="ad9ee-103">Tutorial: Integración de Azure Active Directory con SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="ad9ee-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="ad9ee-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate SciQuest dedicar Director con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad9ee-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="ad9ee-105">Integración SciQuest dedicar Director con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="ad9ee-106">Puede controlar en Azure AD que tenga acceso tooSciQuest Director de gastos</span><span class="sxs-lookup"><span data-stu-id="ad9ee-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="ad9ee-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSciQuest Director de gastos (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ee-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="ad9ee-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="ad9ee-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="ad9ee-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad9ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad9ee-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ad9ee-110">Prerequisites</span></span>
<span data-ttu-id="ad9ee-111">tooconfigure integración de Azure AD con SciQuest dedicar Director, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="ad9ee-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ee-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ad9ee-113">Una suscripción de SciQuest Spend Director habilitada para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ad9ee-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad9ee-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="ad9ee-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ad9ee-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ad9ee-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad9ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="ad9ee-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ad9ee-118">Scenario Description</span></span>
<span data-ttu-id="ad9ee-119">objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="ad9ee-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad9ee-121">Agregar SciQuest dedicar Director de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ad9ee-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="ad9ee-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="ad9ee-123">Agregar SciQuest dedicar Director de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ad9ee-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="ad9ee-124">integración de hello tooconfigure de Director de dedicar SciQuest en Azure AD, deberá tooadd SciQuest dedicar Director de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad9ee-125">**tooadd SciQuest dedicar Director de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ad9ee-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ee-126">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="ad9ee-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="ad9ee-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicaciones][2]

4. <span data-ttu-id="ad9ee-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3]

5. <span data-ttu-id="ad9ee-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicaciones][4]

6. <span data-ttu-id="ad9ee-135">En el cuadro de búsqueda de hello, escriba **sciQuest dedicar director**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Aplicaciones][5]

7. <span data-ttu-id="ad9ee-137">En el panel de resultados de hello, seleccione **SciQuest dedicar Director**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplicaciones][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad9ee-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ee-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad9ee-140">objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con SciQuest dedicar Director a partir de un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad9ee-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad9ee-141">Para toowork de inicio de sesión único, Azure AD necesita tooknow es qué usuario equivalente de hello en Director de gasto de SciQuest tooan usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="ad9ee-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SciQuest dedicar Director debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="ad9ee-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en SciQuest dedicar Director.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="ad9ee-144">tooconfigure y prueba de inicio de sesión único en Azure AD con SciQuest dedicar Director, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad9ee-145">**[Configuración de Azure AD único Single Sign-On](#configuring-azure-ad-single-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad9ee-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad9ee-147">**[Crear un usuario de prueba de Director de gasto de SciQuest](#creating-a-halogen-software-test-user) ** -toohave un equivalente de Britta Simon en SciQuest dedicar Director es representación toohello vinculado Azure AD de ella.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ad9ee-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad9ee-149">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="ad9ee-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ee-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="ad9ee-151">objetivo de Hola de esta sección es tooenable Azure AD single sign-on Hola portal de Azure clásico y tooconfigure inicio de sesión único en la aplicación SciQuest dedicar Director.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="ad9ee-152">**tooconfigure inicio de sesión único en Azure AD con SciQuest dedicar Director, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ad9ee-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ee-153">En el portal de Azure clásico en Hola Hola **SciQuest dedicar Director** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][8]

2. <span data-ttu-id="ad9ee-155">En hello **¿cómo desea que los usuarios toosign en tooSciQuest Director de gastos** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][9]

3. <span data-ttu-id="ad9ee-157">En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Configurar las opciones de la aplicación][10]
   
     <span data-ttu-id="ad9ee-159">a.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-159">a.</span></span> <span data-ttu-id="ad9ee-160">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL que utilizan su toosign a los usuarios de aplicación de Director de gasto de SciQuest de tooyour utiliza Hola siguiente patrón: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="ad9ee-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="ad9ee-161">b.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-161">b.</span></span> <span data-ttu-id="ad9ee-162">Hola **dirección URL de respuesta** cuadro de texto, hello tipo mismo valor ha escrito en hello **dirección URL de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="ad9ee-163">c.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-163">c.</span></span> <span data-ttu-id="ad9ee-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-164">Click **Next**.</span></span>

4. <span data-ttu-id="ad9ee-165">En hello **configurar inicio de sesión único en el Director de dedicar SciQuest** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos de hello localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Qué es Azure AD Connect][11]

5. <span data-ttu-id="ad9ee-167">Póngase en contacto con SciQuest tooenable de compatibilidad con este método de autenticación mediante metadatos de hello anterior descargado.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="ad9ee-168">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Qué es Azure AD Connect][15]

7. <span data-ttu-id="ad9ee-170">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad9ee-171">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ee-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad9ee-172">objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="ad9ee-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ad9ee-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ee-174">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Qué es Azure AD Connect][100] 

2. <span data-ttu-id="ad9ee-176">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="ad9ee-177">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Qué es Azure AD Connect][101] 

4. <span data-ttu-id="ad9ee-179">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Qué es Azure AD Connect][102] 

5. <span data-ttu-id="ad9ee-181">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Qué es Azure AD Connect][103] 
   
    <span data-ttu-id="ad9ee-183">a.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-183">a.</span></span> <span data-ttu-id="ad9ee-184">En **Tipo de usuario**, seleccione **Nuevo usuario de la organización**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="ad9ee-185">b.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-185">b.</span></span> <span data-ttu-id="ad9ee-186">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="ad9ee-187">c.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-187">c.</span></span> <span data-ttu-id="ad9ee-188">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-188">Click **Next**.</span></span>

6. <span data-ttu-id="ad9ee-189">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Qué es Azure AD Connect][104] 
   
    <span data-ttu-id="ad9ee-191">a.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-191">a.</span></span> <span data-ttu-id="ad9ee-192">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="ad9ee-193">b.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-193">b.</span></span> <span data-ttu-id="ad9ee-194">Hola **Last Name** txtbox, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="ad9ee-195">c.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-195">c.</span></span> <span data-ttu-id="ad9ee-196">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="ad9ee-197">d.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-197">d.</span></span> <span data-ttu-id="ad9ee-198">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="ad9ee-199">e.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-199">e.</span></span> <span data-ttu-id="ad9ee-200">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-200">Click **Next**.</span></span>

7. <span data-ttu-id="ad9ee-201">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Qué es Azure AD Connect][105]  

8. <span data-ttu-id="ad9ee-203">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ad9ee-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Qué es Azure AD Connect][106]   
   
    <span data-ttu-id="ad9ee-205">a.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-205">a.</span></span> <span data-ttu-id="ad9ee-206">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="ad9ee-207">b.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-207">b.</span></span> <span data-ttu-id="ad9ee-208">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="ad9ee-209">Creación de un usuario de prueba de SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="ad9ee-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="ad9ee-210">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en SciQuest dedicar Director.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="ad9ee-211">El equipo de soporte de SciQuest dedicar Director es necesario toocontact y proporcionarles detalles Hola sobre su tooget de cuenta de prueba que creó.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="ad9ee-212">Como alternativa, también puede aprovechar el aprovisionamiento Just-In-Time, una característica de inicio de sesión único que es compatible con SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="ad9ee-213">Si el aprovisionamiento Just-In-Time está habilitado, los usuarios se crean automáticamente en SciQuest Spend Director durante un intento de inicio de sesión único, si no existen.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="ad9ee-214">Esta característica elimina la necesidad de hello toomanually crear equivalente de inicio de sesión único a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="ad9ee-215">el aprovisionamiento de just-in-time de tooget habilitado, debe toocontact está el equipo de soporte de SciQuest dedicar Director.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad9ee-216">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ee-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="ad9ee-217">objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSciQuest acceso Director de gastos.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Qué es Azure AD Connect][200]

<span data-ttu-id="ad9ee-219">**tooassign Britta Simon tooSciQuest Director de gasto, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ad9ee-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ee-220">En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Qué es Azure AD Connect][201]

2. <span data-ttu-id="ad9ee-222">En la lista de aplicaciones de hello, seleccione **SciQuest dedicar Director**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Qué es Azure AD Connect][202]

3. <span data-ttu-id="ad9ee-224">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Qué es Azure AD Connect][203]

4. <span data-ttu-id="ad9ee-226">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Qué es Azure AD Connect][204]

5. <span data-ttu-id="ad9ee-228">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Qué es Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="ad9ee-230">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ad9ee-230">Testing Single Sign-On</span></span>
<span data-ttu-id="ad9ee-231">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="ad9ee-232">Al hacer clic en icono de Director de dedicar SciQuest Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour SciQuest dedicar Director aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad9ee-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ad9ee-233">Additional Resources</span></span>
* [<span data-ttu-id="ad9ee-234">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad9ee-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad9ee-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad9ee-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

