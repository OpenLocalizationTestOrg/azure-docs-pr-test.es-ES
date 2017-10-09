---
title: "Tutorial: Integración de Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y FirmPlay - apoyo de empleado de contratación."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="38cd7-103">Tutorial: Integración de Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="38cd7-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="38cd7-104">En este tutorial, aprenderá cómo toointegrate FirmPlay - apoyo de empleado de contratación con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38cd7-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38cd7-105">Integrar FirmPlay - apoyo de empleado de contratación con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="38cd7-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="38cd7-106">Puede controlar en Azure AD que tenga acceso tooFirmPlay - apoyo de empleado de contratación</span><span class="sxs-lookup"><span data-stu-id="38cd7-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="38cd7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFirmPlay - apoyo de empleado de contratación (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cd7-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38cd7-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="38cd7-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="38cd7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38cd7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38cd7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="38cd7-110">Prerequisites</span></span>

<span data-ttu-id="38cd7-111">tooconfigure integración de Azure AD con FirmPlay - apoyo de empleado de contratación, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="38cd7-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="38cd7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cd7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38cd7-113">Una suscripción habilitada para inicio de sesión única de FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="38cd7-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="38cd7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="38cd7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="38cd7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="38cd7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38cd7-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="38cd7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="38cd7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38cd7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="38cd7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="38cd7-118">Scenario description</span></span>
<span data-ttu-id="38cd7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="38cd7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38cd7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="38cd7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38cd7-121">Agregar FirmPlay - apoyo de empleado de contratación de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="38cd7-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="38cd7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cd7-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="38cd7-123">Agregar FirmPlay - apoyo de empleado de contratación de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="38cd7-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="38cd7-124">integración de hello tooconfigure de FirmPlay - Propugnación de empleado de contratación en Azure AD, deberá tooadd FirmPlay - apoyo de empleado de contratación de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="38cd7-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="38cd7-125">**tooadd FirmPlay - apoyo de empleado de contratación de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38cd7-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="38cd7-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="38cd7-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38cd7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="38cd7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="38cd7-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="38cd7-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="38cd7-133">En el cuadro de búsqueda de hello, escriba **FirmPlay - apoyo de empleado de contratación**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="38cd7-135">En el panel de resultados de hello, seleccione **FirmPlay - apoyo de empleado de contratación**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="38cd7-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38cd7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cd7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38cd7-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con FirmPlay - Employee Advocacy for Recruiting utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="38cd7-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38cd7-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en FirmPlay - apoyo de empleado de contratación es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38cd7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="38cd7-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en FirmPlay - apoyo de empleado de contratación debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="38cd7-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="38cd7-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en FirmPlay - apoyo de empleado de contratación.</span><span class="sxs-lookup"><span data-stu-id="38cd7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="38cd7-142">tooconfigure y prueba de inicio de sesión único en Azure AD con FirmPlay - apoyo de empleado de contratación, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="38cd7-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="38cd7-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="38cd7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="38cd7-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38cd7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38cd7-145">**[Crear un FirmPlay - Propugnación empleado para el usuario de prueba de contratación](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave un equivalente de Britta Simon en FirmPlay: Propugnación empleado para aplicaciones de contratación es decir vinculado representación toohello Azure AD de ella.</span><span class="sxs-lookup"><span data-stu-id="38cd7-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="38cd7-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="38cd7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38cd7-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="38cd7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38cd7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cd7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38cd7-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en su FirmPlay - Propugnación empleado para la aplicación de contratación.</span><span class="sxs-lookup"><span data-stu-id="38cd7-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="38cd7-150">**tooconfigure inicio de sesión único en Azure AD con FirmPlay - apoyo de empleado de contratación, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38cd7-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="38cd7-151">En el portal de administración de Azure de hello, en hello **FirmPlay - apoyo de empleado de contratación** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="38cd7-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="38cd7-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="38cd7-155">En hello **FirmPlay - Propugnación empleado para aplicaciones de contratación de dominio y las direcciones URL** sección en hello **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="38cd7-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="38cd7-157">Tenga en cuenta que esto no es un valor real Hola.</span><span class="sxs-lookup"><span data-stu-id="38cd7-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="38cd7-158">Tendrá que tooupdate este valor con hello real iniciar sesión en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="38cd7-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="38cd7-159">Póngase en contacto con [FirmPlay - Propugnación empleado para el equipo de soporte técnico de contratación](mailto:engineering@firmplay.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="38cd7-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="38cd7-160">En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="38cd7-162">En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="38cd7-163">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-163">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="38cd7-165">En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="38cd7-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="38cd7-167">En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="38cd7-169">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="38cd7-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="38cd7-171">En hello **FirmPlay - Propugnación empleado para la configuración de aplicaciones de contratación** sección, haga clic en **FirmPlay configurar - apoyo de empleado de contratación** tooopen **configurar inicio de sesión en**cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38cd7-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="38cd7-174">tooget SSO configurado para la aplicación, póngase en contacto con [FirmPlay - Propugnación empleado para el equipo de soporte técnico de contratación](mailto:engineering@firmplay.com) y proporcionarles siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="38cd7-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="38cd7-175">Hola • descargado **archivo de certificado**</span><span class="sxs-lookup"><span data-stu-id="38cd7-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="38cd7-176">• hello **SAML Single Sign-On dirección URL del servicio**</span><span class="sxs-lookup"><span data-stu-id="38cd7-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="38cd7-177">• hello **Id. de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="38cd7-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="38cd7-178">• hello **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="38cd7-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38cd7-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cd7-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="38cd7-180">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="38cd7-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="38cd7-182">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38cd7-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="38cd7-183">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="38cd7-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38cd7-185">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="38cd7-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38cd7-187">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38cd7-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38cd7-189">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="38cd7-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38cd7-191">a.</span><span class="sxs-lookup"><span data-stu-id="38cd7-191">a.</span></span> <span data-ttu-id="38cd7-192">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38cd7-193">b.</span><span class="sxs-lookup"><span data-stu-id="38cd7-193">b.</span></span> <span data-ttu-id="38cd7-194">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38cd7-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38cd7-195">c.</span><span class="sxs-lookup"><span data-stu-id="38cd7-195">c.</span></span> <span data-ttu-id="38cd7-196">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="38cd7-197">d.</span><span class="sxs-lookup"><span data-stu-id="38cd7-197">d.</span></span> <span data-ttu-id="38cd7-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="38cd7-199">Creación de un usuario de prueba de FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="38cd7-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="38cd7-200">En esta sección, creará un usuario llamado a Britta Simon en FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="38cd7-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="38cd7-201">Trabaje con [FirmPlay - Propugnación empleado para el equipo de soporte técnico de contratación](mailto:engineering@firmplay.com) a los usuarios de tooadd Hola Hola FirmPlay - Propugnación empleado para la plataforma de contratación.</span><span class="sxs-lookup"><span data-stu-id="38cd7-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="38cd7-202">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cd7-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="38cd7-203">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooFirmPlay de acceso - apoyo de empleado de contratación.</span><span class="sxs-lookup"><span data-stu-id="38cd7-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="38cd7-205">**tooassign Britta Simon tooFirmPlay - apoyo de empleado de contratación, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="38cd7-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="38cd7-206">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="38cd7-208">En la lista de aplicaciones de hello, seleccione **FirmPlay - apoyo de empleado de contratación**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="38cd7-210">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="38cd7-212">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-212">Click **Add** button.</span></span> <span data-ttu-id="38cd7-213">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="38cd7-215">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="38cd7-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="38cd7-216">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38cd7-217">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="38cd7-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="38cd7-218">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="38cd7-218">Testing single sign-on</span></span>

<span data-ttu-id="38cd7-219">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="38cd7-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="38cd7-220">Al hacer clic en hello FirmPlay - apoyo de empleado de icono de contratación Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour FirmPlay - Propugnación empleado para la aplicación de contratación.</span><span class="sxs-lookup"><span data-stu-id="38cd7-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="38cd7-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="38cd7-221">Additional resources</span></span>

* [<span data-ttu-id="38cd7-222">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38cd7-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38cd7-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38cd7-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png