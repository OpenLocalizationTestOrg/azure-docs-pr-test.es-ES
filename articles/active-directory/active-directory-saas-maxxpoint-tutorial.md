---
title: "Tutorial: Integración de Azure Active Directory con MaxxPoint | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 03b13908add8d8c62f1d1480ed2288658fce14d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="e8def-103">Tutorial: Integración de Azure Active Directory con MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="e8def-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="e8def-104">En este tutorial, aprenderá cómo toointegrate MaxxPoint con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8def-104">In this tutorial, you learn how toointegrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8def-105">Integración MaxxPoint con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e8def-105">Integrating MaxxPoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e8def-106">Puede controlar en Azure AD que tenga acceso tooMaxxPoint</span><span class="sxs-lookup"><span data-stu-id="e8def-106">You can control in Azure AD who has access tooMaxxPoint</span></span>
- <span data-ttu-id="e8def-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMaxxPoint (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8def-107">You can enable your users tooautomatically get signed-on tooMaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8def-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e8def-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e8def-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8def-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8def-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e8def-110">Prerequisites</span></span>

<span data-ttu-id="e8def-111">integración de Azure AD con MaxxPoint tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e8def-111">tooconfigure Azure AD integration with MaxxPoint, you need hello following items:</span></span>

- <span data-ttu-id="e8def-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8def-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8def-113">Una suscripción habilitada para el inicio de sesión único en MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="e8def-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8def-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e8def-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8def-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e8def-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8def-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e8def-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e8def-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8def-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8def-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e8def-118">Scenario description</span></span>
<span data-ttu-id="e8def-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e8def-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8def-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e8def-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8def-121">Agregar MaxxPoint desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e8def-121">Adding MaxxPoint from hello gallery</span></span>
2. <span data-ttu-id="e8def-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8def-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-hello-gallery"></a><span data-ttu-id="e8def-123">Agregar MaxxPoint desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e8def-123">Adding MaxxPoint from hello gallery</span></span>
<span data-ttu-id="e8def-124">integración de hello tooconfigure de MaxxPoint en Azure AD, deberá tooadd MaxxPoint de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e8def-124">tooconfigure hello integration of MaxxPoint into Azure AD, you need tooadd MaxxPoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e8def-125">**tooadd MaxxPoint de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8def-125">**tooadd MaxxPoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8def-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e8def-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8def-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e8def-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e8def-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e8def-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e8def-131">Haga clic en **nueva aplicación** botón en la parte superior de Hola de tooadd nueva aplicación de cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8def-131">Click **New application** button on hello top of dialog tooadd new application.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e8def-133">En el cuadro de búsqueda de hello, escriba **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="e8def-133">In hello search box, type **MaxxPoint**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="e8def-135">En el panel de resultados de hello, seleccione **MaxxPoint**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e8def-135">In hello results panel, select **MaxxPoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8def-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8def-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8def-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con MaxxPoint con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e8def-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8def-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en MaxxPoint es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8def-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MaxxPoint is tooa user in Azure AD.</span></span> <span data-ttu-id="e8def-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en MaxxPoint debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e8def-140">In other words, a link relationship between an Azure AD user and hello related user in MaxxPoint needs toobe established.</span></span>

<span data-ttu-id="e8def-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="e8def-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in MaxxPoint.</span></span>

<span data-ttu-id="e8def-142">tooconfigure y prueba de inicio de sesión único en Azure AD con MaxxPoint, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e8def-142">tooconfigure and test Azure AD single sign-on with MaxxPoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e8def-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e8def-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e8def-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8def-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8def-145">**[Crear un usuario de prueba MaxxPoint](#creating-a-maxxpoint-test-user)**  -toohave un equivalente de Britta Simon en MaxxPoint que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="e8def-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - toohave a counterpart of Britta Simon in MaxxPoint that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="e8def-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e8def-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8def-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e8def-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8def-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8def-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8def-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="e8def-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="e8def-150">**inicio de sesión único en Azure AD tooconfigure con MaxxPoint, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8def-150">**tooconfigure Azure AD single sign-on with MaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8def-151">En el portal de Azure, en Hola Hola **MaxxPoint** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e8def-151">In hello Azure portal, on hello **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e8def-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e8def-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="e8def-155">En hello **MaxxPoint dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**, pero no necesita tooperform todos los pasos.</span><span class="sxs-lookup"><span data-stu-id="e8def-155">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, no need tooperform any steps.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="e8def-157">En hello **MaxxPoint dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e8def-157">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="e8def-159">a.</span><span class="sxs-lookup"><span data-stu-id="e8def-159">a.</span></span> <span data-ttu-id="e8def-160">Haga clic en la opción **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="e8def-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="e8def-161">b.</span><span class="sxs-lookup"><span data-stu-id="e8def-161">b.</span></span> <span data-ttu-id="e8def-162">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="e8def-162">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8def-163">Tenga en cuenta que esto no es un valor real Hola.</span><span class="sxs-lookup"><span data-stu-id="e8def-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="e8def-164">Tendrá que tooupdate este valor con hello real iniciar sesión en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e8def-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="e8def-165">Llame al equipo de MaxxPoint en **888-728-0950** tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="e8def-165">Call MaxxPoint team on **888-728-0950** tooget this value.</span></span>

5. <span data-ttu-id="e8def-166">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e8def-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="e8def-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e8def-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e8def-170">tooget SSO configurado para la aplicación, llame al equipo de soporte técnico de MaxxPoint en **888-728-0950** y podrá ayudarle aún más en cómo se descarga tooprovide ellos Hola **Metadata XML** archivo.</span><span class="sxs-lookup"><span data-stu-id="e8def-170">tooget SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how tooprovide them hello downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="e8def-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e8def-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e8def-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e8def-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e8def-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8def-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8def-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8def-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8def-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e8def-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e8def-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8def-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8def-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e8def-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8def-180">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e8def-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8def-182">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8def-182">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8def-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e8def-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8def-186">a.</span><span class="sxs-lookup"><span data-stu-id="e8def-186">a.</span></span> <span data-ttu-id="e8def-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8def-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8def-188">b.</span><span class="sxs-lookup"><span data-stu-id="e8def-188">b.</span></span> <span data-ttu-id="e8def-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e8def-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8def-190">c.</span><span class="sxs-lookup"><span data-stu-id="e8def-190">c.</span></span> <span data-ttu-id="e8def-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e8def-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e8def-192">d.</span><span class="sxs-lookup"><span data-stu-id="e8def-192">d.</span></span> <span data-ttu-id="e8def-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e8def-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="e8def-194">Creación de un usuario de prueba de MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="e8def-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="e8def-195">En esta sección, creará un usuario llamado Britta Simon en MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="e8def-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="e8def-196">Llame al equipo de soporte técnico de MaxxPoint en **888-728-0950** a los usuarios de tooadd Hola Hola MaxxPoint aplicación.</span><span class="sxs-lookup"><span data-stu-id="e8def-196">Please call MaxxPoint support team on **888-728-0950** tooadd hello users in hello MaxxPoint application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e8def-197">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8def-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e8def-198">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooMaxxPoint de acceso.</span><span class="sxs-lookup"><span data-stu-id="e8def-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooMaxxPoint.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e8def-200">**tooassign Britta Simon tooMaxxPoint, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8def-200">**tooassign Britta Simon tooMaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8def-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e8def-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e8def-203">En la lista de aplicaciones de hello, seleccione **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="e8def-203">In hello applications list, select **MaxxPoint**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="e8def-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e8def-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e8def-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e8def-207">Click **Add** button.</span></span> <span data-ttu-id="e8def-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e8def-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e8def-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8def-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e8def-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e8def-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8def-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e8def-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8def-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e8def-213">Testing single sign-on</span></span>

<span data-ttu-id="e8def-214">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e8def-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e8def-215">Al hacer clic en icono de MaxxPoint Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour MaxxPoint aplicación.</span><span class="sxs-lookup"><span data-stu-id="e8def-215">When you click hello MaxxPoint tile in hello Access Panel, you should get automatically signed-on tooyour MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e8def-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e8def-216">Additional resources</span></span>

* [<span data-ttu-id="e8def-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8def-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8def-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8def-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png