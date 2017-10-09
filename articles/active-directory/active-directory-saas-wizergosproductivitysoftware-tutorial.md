---
title: "Tutorial: Integración de Azure Active Directory con Wizergos Productivity Software | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el Software de productividad de Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="99544-103">Tutorial: integración de Azure Active Directory con Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="99544-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="99544-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate Wizergos Software de productividad con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99544-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99544-105">La integración del Software de productividad Wizergos con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="99544-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="99544-106">Puede controlar en Azure AD que tenga acceso tooWizergos Software de productividad</span><span class="sxs-lookup"><span data-stu-id="99544-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="99544-107">Puede habilitar la get ha iniciado sesión tooWizergos de usuarios tooautomatically Software de productividad inicio de sesión único (SSO) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99544-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="99544-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="99544-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="99544-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99544-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99544-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99544-110">Prerequisites</span></span>
<span data-ttu-id="99544-111">integración de Azure AD con el Software de productividad de Wizergos tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="99544-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="99544-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99544-112">An Azure AD subscription</span></span>
* <span data-ttu-id="99544-113">Un suscripción habilitada para el inicio de sesión único en Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="99544-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="99544-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="99544-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="99544-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="99544-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="99544-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="99544-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="99544-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99544-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99544-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="99544-118">Scenario description</span></span>
<span data-ttu-id="99544-119">objetivo de Hola de este tutorial es tooenable tootest Azure AD SSO en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="99544-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="99544-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="99544-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99544-121">Agregar Software de productividad Wizergos desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="99544-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="99544-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99544-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="99544-123">Agregar Software de productividad Wizergos desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="99544-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="99544-124">integración de hello tooconfigure Wizergos de Software de productividad en Azure AD, deberá tooadd Wizergos Software de productividad de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="99544-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="99544-125">**tooadd Wizergos Software de productividad de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99544-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="99544-126">Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99544-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="99544-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="99544-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="99544-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="99544-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicaciones][2]
4. <span data-ttu-id="99544-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="99544-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="99544-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="99544-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicaciones][4]
6. <span data-ttu-id="99544-135">En el cuadro de búsqueda de hello, escriba **Software de productividad de Wizergos**.</span><span class="sxs-lookup"><span data-stu-id="99544-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="99544-137">En el panel de resultados de hello, seleccione **Software de productividad de Wizergos**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="99544-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Seleccionar aplicación hello en la Galería de Hola](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="99544-139">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99544-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="99544-140">objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de Azure AD SSO con el Software de productividad de Wizergos a partir de un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99544-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99544-141">Para toowork SSO, Azure AD necesita tooknow qué usuario equivalente de hello en usuario de Software de productividad de Wizergos tooan en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99544-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="99544-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el Software de productividad Wizergos debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="99544-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="99544-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** Wizergos software de productividad.</span><span class="sxs-lookup"><span data-stu-id="99544-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="99544-144">tooconfigure y prueba de inicio de sesión único en Azure AD con BynWizergos productividad Softwareder, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="99544-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="99544-145">**[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="99544-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="99544-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99544-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99544-147">**[Crear un usuario de prueba de Software de productividad de Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave un equivalente de Britta Simon Wizergos software de productividad que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="99544-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="99544-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="99544-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99544-149">**[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="99544-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="99544-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99544-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="99544-151">En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación de Software de productividad de Wizergos.</span><span class="sxs-lookup"><span data-stu-id="99544-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="99544-152">**tooconfigure inicio de sesión único en Azure AD con el Software de productividad Wizergos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99544-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="99544-153">En portal clásico de hello, en hello **Software de productividad de Wizergos** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="99544-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][6] 
2. <span data-ttu-id="99544-155">En hello **¿cómo desea que los usuarios toosign en tooWizergos Software de productividad** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**:</span><span class="sxs-lookup"><span data-stu-id="99544-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="99544-157">En hello **configurar opciones de aplicación** página del cuadro de diálogo, haga clic en **siguiente**:</span><span class="sxs-lookup"><span data-stu-id="99544-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="99544-159">En hello **configurar inicio de sesión único en Software de productividad de Wizergos** página, haga clic en **Descargar certificado**y, a continuación, guarde el archivo hello en el equipo:</span><span class="sxs-lookup"><span data-stu-id="99544-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="99544-161">En una ventana del explorador web diferente, inquilino de Software de productividad de Wizergos tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="99544-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="99544-162">En hello hamburguesa menú, seleccione **administración**.</span><span class="sxs-lookup"><span data-stu-id="99544-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="99544-164">En el menú de la izquierda de la página Admin, seleccione **AUTHENTICACIÓN** y haga clic en **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="99544-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="99544-166">Realizar Hola seguir pasos de **autenticación** sección.</span><span class="sxs-lookup"><span data-stu-id="99544-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="99544-168">Haga clic en **cargar** Hola de tooupload botón descarga certificado de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99544-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="99544-169">Hola **dirección URL del emisor** textbox coloca el valor de Hola de **dirección URL del emisor** desde el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99544-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="99544-170">Hola **dirección URL de inicio de sesión único** textbox coloca el valor de Hola de **URL de servicio de inicio de sesión único** desde el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99544-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="99544-171">Hola **dirección URL de cierre de sesión único** textbox coloca el valor de Hola de **dirección URL del servicio de cierre de sesión único** desde el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99544-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="99544-172">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="99544-172">Click **Save** button.</span></span>
9. <span data-ttu-id="99544-173">En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="99544-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][10]
10. <span data-ttu-id="99544-175">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="99544-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="99544-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99544-177">Create an Azure AD test user</span></span>
<span data-ttu-id="99544-178">objetivo de Hola de esta sección es toocreate un usuario de prueba en el portal clásico de hello llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99544-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="99544-180">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99544-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="99544-181">Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99544-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="99544-183">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="99544-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="99544-184">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="99544-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="99544-186">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="99544-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="99544-188">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="99544-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="99544-190">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="99544-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="99544-191">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99544-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="99544-192">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="99544-192">Click **Next**.</span></span>
6. <span data-ttu-id="99544-193">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="99544-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="99544-195">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="99544-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="99544-196">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="99544-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="99544-197">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99544-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="99544-198">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="99544-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="99544-199">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="99544-199">Click **Next**.</span></span>
7. <span data-ttu-id="99544-200">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="99544-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="99544-202">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="99544-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="99544-204">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="99544-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="99544-205">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="99544-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="99544-206">Creación de un usuario de prueba de Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="99544-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="99544-207">En esta sección, creará un usuario llamado Britta Simon en Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99544-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="99544-208">Trabaje con el equipo de soporte técnico de Software de productividad Wizergos a través de [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd los usuarios de hello en la plataforma de Software de productividad Wizergos Hola.</span><span class="sxs-lookup"><span data-stu-id="99544-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="99544-209">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="99544-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="99544-210">objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure SSO mediante la concesión de su Software de productividad de tooWizergos de acceso.</span><span class="sxs-lookup"><span data-stu-id="99544-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Asignar usuario][200]

<span data-ttu-id="99544-212">**tooassign Britta Simon tooWizergos Software de productividad, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99544-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="99544-213">En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="99544-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Asignar usuario][201]
2. <span data-ttu-id="99544-215">En la lista de aplicaciones de hello, seleccione **Software de productividad de Wizergos**.</span><span class="sxs-lookup"><span data-stu-id="99544-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="99544-217">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="99544-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Asignar usuario][203]
4. <span data-ttu-id="99544-219">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99544-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="99544-220">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="99544-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="99544-222">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="99544-222">Test single sign-on</span></span>
<span data-ttu-id="99544-223">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="99544-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="99544-224">Al hacer clic en icono de Software de productividad Wizergos Hola Hola Panel de acceso, deberá obtener la aplicación de Software de productividad Wizergos tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="99544-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99544-225">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="99544-225">Additional resources</span></span>
* [<span data-ttu-id="99544-226">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99544-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99544-227">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99544-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
