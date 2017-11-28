---
title: "Tutorial: Integración de Azure Active Directory con SensoScientific Wireless Temperature Monitoring System | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el sistema de supervisión de temperatura de SensoScientific inalámbrica."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="5014f-103">Tutorial: Integración de Azure Active Directory con SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="5014f-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="5014f-104">En este tutorial, aprenderá cómo toointegrate SensoScientific inalámbrica temperatura el sistema de supervisión con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5014f-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5014f-105">Integrar el sistema de supervisión de temperatura de SensoScientific inalámbrica con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5014f-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5014f-106">Puede controlar en Azure AD que tenga acceso tooSensoScientific el sistema de supervisión de temperatura de inalámbrica</span><span class="sxs-lookup"><span data-stu-id="5014f-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="5014f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSensoScientific sistema de supervisión de temperatura de inalámbrica (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5014f-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5014f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5014f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5014f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5014f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5014f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5014f-110">Prerequisites</span></span>

<span data-ttu-id="5014f-111">tooconfigure integración de Azure AD con el sistema de supervisión de temperatura de SensoScientific inalámbrica, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5014f-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="5014f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5014f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5014f-113">Una suscripción que tenga habilitado el inicio de sesión único en SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="5014f-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5014f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5014f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5014f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5014f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5014f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5014f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5014f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5014f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5014f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5014f-118">Scenario description</span></span>
<span data-ttu-id="5014f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5014f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5014f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5014f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5014f-121">Agregar el sistema de supervisión de temperatura de SensoScientific inalámbrica desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="5014f-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="5014f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5014f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="5014f-123">Agregar el sistema de supervisión de temperatura de SensoScientific inalámbrica desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="5014f-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="5014f-124">integración de hello tooconfigure del sistema de supervisión de temperatura de SensoScientific inalámbrico en Azure AD, deberá tooadd el sistema de supervisión de temperatura de SensoScientific inalámbrico de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5014f-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5014f-125">**tooadd SensoScientific inalámbrica temperatura el sistema de supervisión de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5014f-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5014f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5014f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5014f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5014f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5014f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5014f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5014f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5014f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5014f-133">En el cuadro de búsqueda de hello, escriba **el sistema de supervisión de temperatura de SensoScientific inalámbrica**.</span><span class="sxs-lookup"><span data-stu-id="5014f-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="5014f-135">En el panel de resultados de hello, seleccione **el sistema de supervisión de temperatura de SensoScientific inalámbrica**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5014f-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5014f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5014f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5014f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SensoScientific Wireless Temperature Monitoring System mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5014f-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5014f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el sistema de supervisión de temperatura de SensoScientific inalámbrica es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5014f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="5014f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el sistema de supervisión de temperatura de SensoScientific inalámbrica debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="5014f-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="5014f-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en el sistema de supervisión de temperatura de SensoScientific inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="5014f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="5014f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con el sistema de supervisión de temperatura de SensoScientific inalámbrica, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5014f-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5014f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="5014f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5014f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5014f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5014f-145">**[Crear un usuario de prueba del sistema de supervisión de temperatura de SensoScientific inalámbrica](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave un equivalente de Britta Simon en SensoScientific inalámbrica temperatura el sistema de supervisión que está vinculado representación toohello Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="5014f-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5014f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5014f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5014f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5014f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5014f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5014f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5014f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de sistema de supervisión de temperatura de SensoScientific inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="5014f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="5014f-150">**tooconfigure inicio de sesión único en Azure AD con el sistema de supervisión de una temperatura de Wireless SensoScientific, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5014f-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="5014f-151">En el portal de Azure, en Hola Hola **el sistema de supervisión de temperatura de SensoScientific inalámbrica** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5014f-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5014f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5014f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="5014f-155">En hello **SensoScientific inalámbrica temperatura el dominio de sistema de supervisión y las direcciones URL** no sección ningún tooperform necesario ningún paso como aplicación hello ya está integrado previamente con Azure:</span><span class="sxs-lookup"><span data-stu-id="5014f-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="5014f-157">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5014f-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="5014f-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5014f-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5014f-161">En hello **configuración de sistema de supervisión de SensoScientific inalámbrica temperatura** sección, haga clic en **configurar sistema de supervisión de SensoScientific inalámbrica temperatura** tooopen  **Configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="5014f-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5014f-162">Hola copia **dirección URL de cierre de sesión, Id. de entidad SAML** y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="5014f-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="5014f-164">Inicie sesión en tooyour aplicación del sistema de supervisión de temperatura de SensoScientific inalámbrica como administrador.</span><span class="sxs-lookup"><span data-stu-id="5014f-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="5014f-165">En el menú de navegación de hello en la parte superior de hello, haga clic en **configuración** y goto **configurar** en **Single Sign On** tooopen Hola inicio de sesión único en la configuración.</span><span class="sxs-lookup"><span data-stu-id="5014f-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="5014f-167">En **inicio de sesión único en la configuración** formulario realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5014f-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="5014f-168">a.</span><span class="sxs-lookup"><span data-stu-id="5014f-168">a.</span></span> <span data-ttu-id="5014f-169">Seleccione **Issuer Name** (Nombre del emisor) como Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5014f-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="5014f-170">b.</span><span class="sxs-lookup"><span data-stu-id="5014f-170">b.</span></span> <span data-ttu-id="5014f-171">Hola pegar **Id. de entidad SAML** que haya copiado desde el portal de Azure en el cuadro de texto de dirección URL del emisor.</span><span class="sxs-lookup"><span data-stu-id="5014f-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="5014f-172">c.</span><span class="sxs-lookup"><span data-stu-id="5014f-172">c.</span></span> <span data-ttu-id="5014f-173">Hola pegar **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure en el cuadro de texto URL de servicio de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5014f-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="5014f-174">d.</span><span class="sxs-lookup"><span data-stu-id="5014f-174">d.</span></span> <span data-ttu-id="5014f-175">Hola pegar **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure en el cuadro de texto de dirección URL del servicio de cierre de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5014f-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="5014f-176">e.</span><span class="sxs-lookup"><span data-stu-id="5014f-176">e.</span></span> <span data-ttu-id="5014f-177">Examinar el certificado de Hola que ha descargado desde el portal de Azure y cargar aquí.</span><span class="sxs-lookup"><span data-stu-id="5014f-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="5014f-178">f.</span><span class="sxs-lookup"><span data-stu-id="5014f-178">f.</span></span> <span data-ttu-id="5014f-179">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5014f-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="5014f-180">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="5014f-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5014f-181">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="5014f-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5014f-182">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5014f-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5014f-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5014f-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="5014f-184">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="5014f-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5014f-186">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5014f-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5014f-187">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5014f-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5014f-189">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5014f-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5014f-191">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5014f-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5014f-193">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5014f-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5014f-195">a.</span><span class="sxs-lookup"><span data-stu-id="5014f-195">a.</span></span> <span data-ttu-id="5014f-196">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5014f-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5014f-197">b.</span><span class="sxs-lookup"><span data-stu-id="5014f-197">b.</span></span> <span data-ttu-id="5014f-198">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5014f-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5014f-199">c.</span><span class="sxs-lookup"><span data-stu-id="5014f-199">c.</span></span> <span data-ttu-id="5014f-200">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5014f-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5014f-201">d.</span><span class="sxs-lookup"><span data-stu-id="5014f-201">d.</span></span> <span data-ttu-id="5014f-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5014f-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="5014f-203">Creación de un usuario de prueba de SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="5014f-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="5014f-204">toolog de los usuarios de Azure AD tooenable en tooSensoScientific el sistema de supervisión de temperatura de inalámbrica, se les debe aprovisionar en el sistema de supervisión de temperatura de SensoScientific inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="5014f-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="5014f-205">Trabajar con [equipo de soporte técnico del sistema de supervisión de temperatura de SensoScientific Wireless](https://www.sensoscientific.com/contact-us/) para agregar usuarios de hello en la plataforma del sistema de supervisión de temperatura de SensoScientific inalámbrica Hola.</span><span class="sxs-lookup"><span data-stu-id="5014f-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="5014f-206">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5014f-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5014f-207">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5014f-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5014f-208">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSensoScientific el sistema de supervisión de temperatura de inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="5014f-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5014f-210">**tooassign Britta Simon tooSensoScientific sistema de supervisión de temperatura de inalámbrica, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5014f-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="5014f-211">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5014f-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5014f-213">En la lista de aplicaciones de hello, seleccione **el sistema de supervisión de temperatura de SensoScientific inalámbrica**.</span><span class="sxs-lookup"><span data-stu-id="5014f-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="5014f-215">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5014f-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5014f-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5014f-217">Click **Add** button.</span></span> <span data-ttu-id="5014f-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5014f-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5014f-220">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5014f-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5014f-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5014f-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5014f-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5014f-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5014f-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5014f-223">Testing single sign-on</span></span>

<span data-ttu-id="5014f-224">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5014f-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="5014f-225">Haga clic en icono de sistema de supervisión de temperatura de SensoScientific inalámbrica Hola Hola Panel de acceso, será la aplicación de sistema de supervisión de temperatura de SensoScientific inalámbrica tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="5014f-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="5014f-226">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="5014f-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5014f-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5014f-227">Additional resources</span></span>

* [<span data-ttu-id="5014f-228">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5014f-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5014f-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5014f-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

