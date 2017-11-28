---
title: "Tutorial: Integración de Azure Active Directory con PurelyHR | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="86200-103">Tutorial: Integración de Azure Active Directory con PurelyHR</span><span class="sxs-lookup"><span data-stu-id="86200-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="86200-104">En este tutorial, aprenderá cómo toointegrate PurelyHR con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86200-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86200-105">Integración PurelyHR con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="86200-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86200-106">Puede controlar en Azure AD que tenga acceso tooPurelyHR</span><span class="sxs-lookup"><span data-stu-id="86200-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="86200-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPurelyHR (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86200-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86200-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="86200-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="86200-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86200-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86200-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="86200-110">Prerequisites</span></span>

<span data-ttu-id="86200-111">integración de Azure AD con PurelyHR tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="86200-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="86200-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86200-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86200-113">Una suscripción habilitada para inicio de sesión único en PurelyHR</span><span class="sxs-lookup"><span data-stu-id="86200-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86200-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="86200-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86200-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="86200-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86200-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="86200-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86200-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86200-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86200-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="86200-118">Scenario description</span></span>
<span data-ttu-id="86200-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="86200-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86200-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="86200-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86200-121">Agregar PurelyHR desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="86200-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="86200-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86200-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="86200-123">Agregar PurelyHR desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="86200-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="86200-124">integración de hello tooconfigure de PurelyHR en Azure AD, deberá tooadd PurelyHR de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="86200-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86200-125">**tooadd PurelyHR de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86200-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86200-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="86200-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86200-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="86200-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86200-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="86200-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="86200-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86200-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="86200-133">En el cuadro de búsqueda de hello, escriba **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="86200-133">In hello search box, type **PurelyHR**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="86200-135">En el panel de resultados de hello, seleccione **PurelyHR**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="86200-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86200-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86200-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86200-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con PurelyHR con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="86200-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86200-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PurelyHR es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86200-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="86200-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PurelyHR debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="86200-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="86200-141">En PurelyHR, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="86200-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="86200-142">tooconfigure y prueba de inicio de sesión único en Azure AD con PurelyHR, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="86200-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86200-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="86200-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86200-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86200-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86200-145">**[Crear un usuario de prueba PurelyHR](#creating-a-purelyhr-test-user)**  -toohave un equivalente de Britta Simon en PurelyHR que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="86200-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="86200-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="86200-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86200-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="86200-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86200-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86200-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86200-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="86200-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="86200-150">**inicio de sesión único en Azure AD tooconfigure con PurelyHR, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86200-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="86200-151">En el portal de Azure, en Hola Hola **PurelyHR** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="86200-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="86200-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="86200-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="86200-155">En hello **PurelyHR dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="86200-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="86200-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="86200-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="86200-158">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="86200-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="86200-160">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="86200-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="86200-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="86200-161">These values are not hello real.</span></span> <span data-ttu-id="86200-162">Actualizar estos valores con la dirección URL de respuesta real hello y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="86200-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="86200-163">Póngase en contacto con [equipo de soporte técnico de cliente de PurelyHR](http://support.purelyhr.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="86200-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="86200-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="86200-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="86200-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="86200-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="86200-168">En hello **PurelyHR configuración** sección, haga clic en **configurar PurelyHR** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="86200-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="86200-169">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="86200-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="86200-171">inicio de sesión único en tooconfigure en **PurelyHR** lado, el sitio Web de tootheir de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="86200-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="86200-172">Abra hello **panel** de opciones de hello en la barra de herramientas de Hola y haga clic en **configuración de SSO**.</span><span class="sxs-lookup"><span data-stu-id="86200-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="86200-173">Describen los valores de hello pegar Hola que en los cuadros siguientes:</span><span class="sxs-lookup"><span data-stu-id="86200-173">Paste hello values in hello boxes as described below-</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="86200-175">a.</span><span class="sxs-lookup"><span data-stu-id="86200-175">a.</span></span> <span data-ttu-id="86200-176">Abra hello **Certificate(Bas64)** descargado de hello portal de Azure en el Bloc de notas y copie valor de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="86200-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="86200-177">Hola pegar copia valor en hello **certificado X.509** cuadro.</span><span class="sxs-lookup"><span data-stu-id="86200-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="86200-178">b.</span><span class="sxs-lookup"><span data-stu-id="86200-178">b.</span></span> <span data-ttu-id="86200-179">Hola **dirección URL del emisor de Idp** cuadro, pegue hello **Id. de entidad SAML** copiados de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="86200-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="86200-180">c.</span><span class="sxs-lookup"><span data-stu-id="86200-180">c.</span></span> <span data-ttu-id="86200-181">Hola **dirección URL del extremo Idp** cuadro, pegue hello **SAML Single Sign-On dirección URL del servicio** copiados de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="86200-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="86200-182">d.</span><span class="sxs-lookup"><span data-stu-id="86200-182">d.</span></span> <span data-ttu-id="86200-183">Comprobar hello **crear usuarios automáticamente** aprovisionamiento de casilla de verificación tooenable automático de usuarios en PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="86200-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="86200-184">e.</span><span class="sxs-lookup"><span data-stu-id="86200-184">e.</span></span> <span data-ttu-id="86200-185">Haga clic en **guardar cambios** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="86200-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="86200-186">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="86200-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86200-187">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="86200-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86200-188">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86200-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86200-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86200-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="86200-190">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="86200-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="86200-192">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86200-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86200-193">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="86200-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86200-195">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="86200-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86200-197">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="86200-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86200-199">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="86200-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86200-201">a.</span><span class="sxs-lookup"><span data-stu-id="86200-201">a.</span></span> <span data-ttu-id="86200-202">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86200-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86200-203">b.</span><span class="sxs-lookup"><span data-stu-id="86200-203">b.</span></span> <span data-ttu-id="86200-204">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86200-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86200-205">c.</span><span class="sxs-lookup"><span data-stu-id="86200-205">c.</span></span> <span data-ttu-id="86200-206">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="86200-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="86200-207">d.</span><span class="sxs-lookup"><span data-stu-id="86200-207">d.</span></span> <span data-ttu-id="86200-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="86200-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="86200-209">Creación de un usuario de prueba en PurelyHR</span><span class="sxs-lookup"><span data-stu-id="86200-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="86200-210">toolog de los usuarios de Azure AD tooenable en tooPurelyHR, se les deben aprovisionar en PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="86200-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="86200-211">En PurelyHR, el aprovisionamiento es una tarea automática y no se requieren pasos manuales al habilitar el aprovisionamiento automático de usuarios.</span><span class="sxs-lookup"><span data-stu-id="86200-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="86200-212">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="86200-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="86200-213">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPurelyHR.</span><span class="sxs-lookup"><span data-stu-id="86200-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="86200-215">**tooassign Britta Simon tooPurelyHR, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86200-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="86200-216">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="86200-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="86200-218">En la lista de aplicaciones de hello, seleccione **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="86200-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="86200-220">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="86200-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="86200-222">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="86200-222">Click **Add** button.</span></span> <span data-ttu-id="86200-223">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="86200-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="86200-225">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="86200-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86200-226">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="86200-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86200-227">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="86200-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86200-228">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="86200-228">Testing single sign-on</span></span>

<span data-ttu-id="86200-229">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="86200-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="86200-230">Haga clic en hello absorber LMS disponer en mosaico en hello Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour LMS absorber la aplicación.</span><span class="sxs-lookup"><span data-stu-id="86200-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="86200-231">Para obtener más información acerca de hello Panel de acceso, consulte.</span><span class="sxs-lookup"><span data-stu-id="86200-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="86200-232">[Introducción toohello Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="86200-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86200-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="86200-233">Additional resources</span></span>

* [<span data-ttu-id="86200-234">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86200-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86200-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86200-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

