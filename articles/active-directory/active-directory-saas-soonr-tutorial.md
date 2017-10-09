---
title: "Tutorial: integración de Azure Active Directory con Soonr Workplace | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Soonr al área de trabajo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="7d1c6-103">Tutorial: integración de Azure Active Directory con Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="7d1c6-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="7d1c6-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate Soonr al área de trabajo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d1c6-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="7d1c6-105">Integración Soonr al área de trabajo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d1c6-106">Puede controlar en Azure AD que tenga acceso tooSoonr al área de trabajo</span><span class="sxs-lookup"><span data-stu-id="7d1c6-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="7d1c6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSoonr al área de trabajo (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d1c6-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d1c6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="7d1c6-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="7d1c6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d1c6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d1c6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7d1c6-110">Prerequisites</span></span>

<span data-ttu-id="7d1c6-111">integración de Azure AD con un área de trabajo de Soonr tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="7d1c6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d1c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d1c6-113">Una suscripción habilitada para inicio de sesión único en Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="7d1c6-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="7d1c6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7d1c6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d1c6-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7d1c6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d1c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7d1c6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7d1c6-118">Scenario description</span></span>
<span data-ttu-id="7d1c6-119">objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="7d1c6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d1c6-121">Agregar un área de trabajo Soonr de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7d1c6-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="7d1c6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d1c6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="7d1c6-123">Agregar un área de trabajo Soonr de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7d1c6-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="7d1c6-124">integración de hello tooconfigure Soonr área de trabajo en Azure AD, deberá tooadd Soonr al área de trabajo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d1c6-125">**tooadd Soonr al área de trabajo desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d1c6-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d1c6-126">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d1c6-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="7d1c6-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplicaciones][2]

4. <span data-ttu-id="7d1c6-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplicaciones][3]

5. <span data-ttu-id="7d1c6-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Aplicaciones][4]

6. <span data-ttu-id="7d1c6-135">En el cuadro de búsqueda de hello, escriba **al área de trabajo de Soonr**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="7d1c6-137">En el panel de resultados de hello, seleccione **al área de trabajo de Soonr**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d1c6-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d1c6-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d1c6-140">objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con Soonr al área de trabajo a partir de un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7d1c6-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d1c6-141">Para toowork de inicio de sesión único, Azure AD necesita tooknow es qué usuario equivalente de hello en usuario de un área de trabajo de Soonr tooan en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="7d1c6-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el área de trabajo de Soonr debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="7d1c6-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en lugar de trabajo Soonr.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="7d1c6-144">tooconfigure y prueba de inicio de sesión único en Azure AD con Soonr al área de trabajo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d1c6-145">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d1c6-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d1c6-147">**[Crear un usuario de prueba al área de trabajo de Soonr](#creating-a-soonr-workplace-test-user)**  -toohave un equivalente de Britta Simon en lugar de trabajo de Soonr es representación toohello vinculado Azure AD de ella.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7d1c6-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d1c6-149">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d1c6-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d1c6-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d1c6-151">En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación de área de trabajo de Soonr.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="7d1c6-152">**inicio de sesión único en tooconfigure Azure AD con Soonr al área de trabajo, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d1c6-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d1c6-153">En el portal de Azure clásico en Hola Hola **al área de trabajo de Soonr** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Configurar inicio de sesión único][6] 

2. <span data-ttu-id="7d1c6-155">En hello **¿cómo desea que los usuarios toosign en tooSoonr al área de trabajo** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="7d1c6-157">En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="7d1c6-159">a.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-159">a.</span></span> <span data-ttu-id="7d1c6-160">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="7d1c6-161">b.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-161">b.</span></span> <span data-ttu-id="7d1c6-162">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7d1c6-163">Tenga en cuenta que esto no es un valor real Hola.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="7d1c6-164">Tendrá que tooupdate este valor con hello real iniciar sesión en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="7d1c6-165">Póngase en contacto con tooget de equipo de soporte técnico al área de trabajo de Soonr este valor.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="7d1c6-166">En hello **configurar inicio de sesión único en el área de trabajo de Soonr** página, haga clic en **descargar metadatos** y, a continuación, guarde el archivo hello en el equipo:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="7d1c6-168">tooget SSO configurado para la aplicación, póngase en contacto con el equipo de soporte técnico al área de trabajo Soonr y proporcionarles siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="7d1c6-169">Hola • descargado **metadatos** archivo</span><span class="sxs-lookup"><span data-stu-id="7d1c6-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="7d1c6-170">• hello **dirección URL del emisor**</span><span class="sxs-lookup"><span data-stu-id="7d1c6-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="7d1c6-171">• hello **dirección URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="7d1c6-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="7d1c6-172">• hello **dirección URL del servicio de cierre de sesión único**</span><span class="sxs-lookup"><span data-stu-id="7d1c6-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="7d1c6-173">Esta aplicación es sustituida por <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">al área de trabajo de Autotask</a> y hacer referencia <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">esto</a> tutorial para configurar la aplicación hello con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="7d1c6-174">Hola portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Inicio de sesión único de Azure AD ][10]

7. <span data-ttu-id="7d1c6-176">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Inicio de sesión único de Azure AD ][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d1c6-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d1c6-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d1c6-179">objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="7d1c6-181">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d1c6-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d1c6-182">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="7d1c6-184">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="7d1c6-185">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d1c6-187">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="7d1c6-189">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="7d1c6-191">a.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-191">a.</span></span> <span data-ttu-id="7d1c6-192">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="7d1c6-193">b.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-193">b.</span></span> <span data-ttu-id="7d1c6-194">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d1c6-195">c.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-195">c.</span></span> <span data-ttu-id="7d1c6-196">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-196">Click **Next**.</span></span>

6.  <span data-ttu-id="7d1c6-197">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="7d1c6-199">a.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-199">a.</span></span> <span data-ttu-id="7d1c6-200">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="7d1c6-201">b.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-201">b.</span></span> <span data-ttu-id="7d1c6-202">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="7d1c6-203">c.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-203">c.</span></span> <span data-ttu-id="7d1c6-204">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="7d1c6-205">d.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-205">d.</span></span> <span data-ttu-id="7d1c6-206">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="7d1c6-207">e.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-207">e.</span></span> <span data-ttu-id="7d1c6-208">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-208">Click **Next**.</span></span>

7. <span data-ttu-id="7d1c6-209">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="7d1c6-211">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7d1c6-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="7d1c6-213">a.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-213">a.</span></span> <span data-ttu-id="7d1c6-214">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="7d1c6-215">b.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-215">b.</span></span> <span data-ttu-id="7d1c6-216">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="7d1c6-217">Creación de un usuario de prueba de Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="7d1c6-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="7d1c6-218">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en lugar de trabajo de Soonr toocreate.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="7d1c6-219">Trabaje con toocreate de equipo de soporte técnico al área de trabajo de Soonr un usuario en la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="7d1c6-220">Puede generar incidencia de soporte técnico de hello con Soonr de <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">aquí</a>.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7d1c6-221">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d1c6-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7d1c6-222">objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSoonr de acceso al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7d1c6-224">**tooassign Britta Simon tooSoonr al área de trabajo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d1c6-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d1c6-225">En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7d1c6-227">En la lista de aplicaciones de hello, seleccione **al área de trabajo de Soonr**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="7d1c6-229">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-229">In hello menu on hello top, click **Users**.</span></span>

    ![Asignar usuario][203] 

1. <span data-ttu-id="7d1c6-231">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="7d1c6-232">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Asignar usuario][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="7d1c6-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7d1c6-234">Testing single sign-on</span></span>

<span data-ttu-id="7d1c6-235">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="7d1c6-236">Al hacer clic en hello al área de trabajo Soonr el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Soonr al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7d1c6-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7d1c6-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7d1c6-237">Additional resources</span></span>

* [<span data-ttu-id="7d1c6-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d1c6-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d1c6-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7d1c6-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
