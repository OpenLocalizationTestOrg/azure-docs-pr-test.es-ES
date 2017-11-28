---
title: "Tutorial: Integración de Azure Active Directory con Humanity | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y pueda imaginar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="ecb5b-103">Tutorial: Integración de Azure Active Directory con Humanity</span><span class="sxs-lookup"><span data-stu-id="ecb5b-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="ecb5b-104">En este tutorial, aprenderá cómo toointegrate pueda imaginar con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecb5b-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecb5b-105">Integración pueda imaginar con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ecb5b-106">Puede controlar en Azure AD que tenga acceso tooHumanity</span><span class="sxs-lookup"><span data-stu-id="ecb5b-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="ecb5b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHumanity (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb5b-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ecb5b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ecb5b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ecb5b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ecb5b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecb5b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ecb5b-110">Prerequisites</span></span>

<span data-ttu-id="ecb5b-111">integración de Azure AD con pueda imaginar tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="ecb5b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb5b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ecb5b-113">Una suscripción habilitada para el inicio de sesión único en Humanity</span><span class="sxs-lookup"><span data-stu-id="ecb5b-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ecb5b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ecb5b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ecb5b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ecb5b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecb5b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ecb5b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ecb5b-118">Scenario description</span></span>
<span data-ttu-id="ecb5b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ecb5b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ecb5b-121">Agregar pueda imaginar desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ecb5b-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="ecb5b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb5b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="ecb5b-123">Agregar pueda imaginar desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ecb5b-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="ecb5b-124">integración de hello tooconfigure de pueda imaginar en Azure AD, deberá tooadd pueda imaginar de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ecb5b-125">**tooadd pueda imaginar desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ecb5b-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecb5b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ecb5b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ecb5b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ecb5b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ecb5b-133">En el cuadro de búsqueda de hello, escriba **pueda imaginar**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-133">In hello search box, type **Humanity**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="ecb5b-135">En el panel de resultados de hello, seleccione **pueda imaginar**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ecb5b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb5b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ecb5b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Humanity con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ecb5b-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ecb5b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en pueda imaginar es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="ecb5b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en pueda imaginar debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="ecb5b-141">En pueda imaginar, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ecb5b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con pueda imaginar, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ecb5b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ecb5b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ecb5b-145">**[Crear un usuario de prueba pueda imaginar](#creating-a-humanity-test-user)**  -toohave un equivalente de Britta Simon en pueda imaginar que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ecb5b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ecb5b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ecb5b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb5b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ecb5b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación pueda imaginar.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="ecb5b-150">**inicio de sesión único en Azure AD tooconfigure con pueda imaginar, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ecb5b-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecb5b-151">En el portal de Azure, en Hola Hola **pueda imaginar** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ecb5b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="ecb5b-155">En hello **pueda imaginar dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="ecb5b-157">a.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-157">a.</span></span> <span data-ttu-id="ecb5b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="ecb5b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="ecb5b-159">b.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-159">b.</span></span> <span data-ttu-id="ecb5b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="ecb5b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ecb5b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-161">These values are not real.</span></span> <span data-ttu-id="ecb5b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ecb5b-163">Póngase en contacto con [equipo de soporte técnico de cliente pueda imaginar](https://www.humanity.com/support/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="ecb5b-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="ecb5b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ecb5b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ecb5b-168">En hello **configuración pueda imaginar** sección, haga clic en **pueda imaginar configurar** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ecb5b-169">Hola copia **SAML Single Sign-On dirección URL del servicio y la dirección URL de cierre de sesión** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="ecb5b-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="ecb5b-171">En una ventana del explorador web diferente, inicie sesión en tooyour **pueda imaginar** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="ecb5b-172">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="ecb5b-173">![Administración](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="ecb5b-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="ecb5b-174">En **Integración**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="ecb5b-175">![Inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ecb5b-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="ecb5b-176">Hola **Single Sign-On** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ecb5b-177">![Inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ecb5b-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="ecb5b-178">a.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-178">a.</span></span> <span data-ttu-id="ecb5b-179">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="ecb5b-180">b.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-180">b.</span></span> <span data-ttu-id="ecb5b-181">Seleccione **Allow Password Login** (Permitir inicio de sesión de contraseña).</span><span class="sxs-lookup"><span data-stu-id="ecb5b-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="ecb5b-182">c.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-182">c.</span></span> <span data-ttu-id="ecb5b-183">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor en hello **dirección URL del emisor de SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="ecb5b-184">d.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-184">d.</span></span> <span data-ttu-id="ecb5b-185">Hola pegar **dirección URL de cierre de sesión** valor en hello **dirección URL de cierre de sesión remoto** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="ecb5b-186">e.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-186">e.</span></span> <span data-ttu-id="ecb5b-187">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="ecb5b-188">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="ecb5b-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="ecb5b-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ecb5b-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ecb5b-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ecb5b-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ecb5b-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb5b-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="ecb5b-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ecb5b-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ecb5b-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecb5b-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ecb5b-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ecb5b-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ecb5b-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ecb5b-204">a.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-204">a.</span></span> <span data-ttu-id="ecb5b-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ecb5b-206">b.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-206">b.</span></span> <span data-ttu-id="ecb5b-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ecb5b-208">c.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-208">c.</span></span> <span data-ttu-id="ecb5b-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ecb5b-210">d.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-210">d.</span></span> <span data-ttu-id="ecb5b-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="ecb5b-212">Creación de un usuario de prueba de Humanity</span><span class="sxs-lookup"><span data-stu-id="ecb5b-212">Creating a Humanity test user</span></span>

<span data-ttu-id="ecb5b-213">En orden tooenable toolog de los usuarios de Azure AD en tooHumanity, se les deben aprovisionar en pueda imaginar.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="ecb5b-214">En caso de hello de pueda imaginar, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="ecb5b-215">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ecb5b-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecb5b-216">Inicie sesión en tooyour **pueda imaginar** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="ecb5b-217">Haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="ecb5b-218">![Administración](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="ecb5b-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="ecb5b-219">Haga clic en **Personal**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="ecb5b-220">![Personal](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Personal")</span><span class="sxs-lookup"><span data-stu-id="ecb5b-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="ecb5b-221">En **Acciones**, haga clic en **Agregar empleados**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="ecb5b-222">![Agregar empleados](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Agregar empleados")</span><span class="sxs-lookup"><span data-stu-id="ecb5b-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="ecb5b-223">Hola **agregar empleados** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ecb5b-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ecb5b-224">![Guardar empleados](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Guardar empleados")</span><span class="sxs-lookup"><span data-stu-id="ecb5b-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="ecb5b-225">a.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-225">a.</span></span> <span data-ttu-id="ecb5b-226">Hola de tipo **nombre**, **Last Name**, y **correo electrónico** de una cuenta válida de AAD que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="ecb5b-227">b.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-227">b.</span></span> <span data-ttu-id="ecb5b-228">Haga clic en **Guardar empleados**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="ecb5b-229">Puede usar cualquier otra pueda imaginar usuario cuenta herramienta de creación o las API proporcionadas por pueda imaginar tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ecb5b-230">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb5b-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ecb5b-231">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHumanity.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ecb5b-233">**tooassign Britta Simon tooHumanity, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ecb5b-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecb5b-234">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ecb5b-236">En la lista de aplicaciones de hello, seleccione **pueda imaginar**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-236">In hello applications list, select **Humanity**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="ecb5b-238">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ecb5b-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-240">Click **Add** button.</span></span> <span data-ttu-id="ecb5b-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ecb5b-243">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ecb5b-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ecb5b-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ecb5b-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ecb5b-246">Testing single sign-on</span></span>

<span data-ttu-id="ecb5b-247">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ecb5b-248">Al hacer clic en icono de pueda imaginar Hola Hola Panel de acceso, deberá obtener la aplicación pueda imaginar de tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="ecb5b-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="ecb5b-249">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ecb5b-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ecb5b-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ecb5b-250">Additional resources</span></span>

* [<span data-ttu-id="ecb5b-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecb5b-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ecb5b-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ecb5b-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

