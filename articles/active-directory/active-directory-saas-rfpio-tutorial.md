---
title: "Tutorial: Integración de Azure Active Directory con RFPIO | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="9bba4-103">Tutorial: Integración de Azure Active Directory con RFPIO</span><span class="sxs-lookup"><span data-stu-id="9bba4-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="9bba4-104">En este tutorial, aprenderá cómo toointegrate RFPIO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9bba4-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9bba4-105">Integración RFPIO con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9bba4-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9bba4-106">Puede controlar quién en Azure AD que tenga acceso tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="9bba4-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="9bba4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRFPIO (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bba4-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9bba4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bba4-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="9bba4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9bba4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bba4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9bba4-110">Prerequisites</span></span>

<span data-ttu-id="9bba4-111">integración de Azure AD con RFPIO tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9bba4-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="9bba4-112">Una suscripción de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bba4-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="9bba4-113">Una suscripción habilitada para el inicio de sesión único en RFPIO</span><span class="sxs-lookup"><span data-stu-id="9bba4-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="9bba4-114">No se recomienda que utilice un pasos de hello tootest del entorno de producción en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9bba4-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="9bba4-115">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9bba4-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9bba4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9bba4-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="9bba4-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bba4-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9bba4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9bba4-118">Scenario description</span></span>
<span data-ttu-id="9bba4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9bba4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9bba4-120">escenario de Hola que se describe en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9bba4-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9bba4-121">Agregar RFPIO desde la Galería de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bba4-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="9bba4-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bba4-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="9bba4-123">Agregar RFPIO de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9bba4-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="9bba4-124">integración de hello tooconfigure de RFPIO en Azure AD, deberá tooadd RFPIO de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9bba4-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="9bba4-125">tooadd RFPIO de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9bba4-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="9bba4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en Hola panel de navegación izquierdo, seleccione hello **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9bba4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9bba4-128">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9bba4-130">tooadd una nueva aplicación, seleccione hello **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9bba4-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9bba4-132">En el cuadro de búsqueda de hello, escriba **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-132">In hello search box, type **RFPIO**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="9bba4-134">En el panel de resultados de hello, seleccione **RFPIO**y, a continuación, seleccione hello **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9bba4-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9bba4-136">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bba4-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9bba4-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con RFPIO con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9bba4-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9bba4-138">Para toowork de inicio de sesión único, Azure AD necesita tooknow ¿qué relación hello es entre equivalente en RFPIO un usuario y en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bba4-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="9bba4-139">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en RFPIO debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9bba4-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="9bba4-140">En RFPIO, asigne el valor de Hola de **nombre de usuario** en Azure AD como valor de Hola de **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bba4-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9bba4-141">tooconfigure y prueba de inicio de sesión único en Azure AD con RFPIO, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9bba4-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9bba4-142">**[Configurar Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable su toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9bba4-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9bba4-143">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**--tootest inicio de sesión único en Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9bba4-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9bba4-144">**[Crear un usuario de prueba RFPIO](#creating-a-rfpio-test-user)**  --toohave un equivalente de Britta Simon en RFPIO que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9bba4-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9bba4-145">**[Asignar el usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**tooenable--Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9bba4-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9bba4-146">**[Probar el inicio de sesión único](#testing-single-sign-on)**  --tooverify si Hola configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="9bba4-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9bba4-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bba4-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9bba4-148">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación RFPIO.</span><span class="sxs-lookup"><span data-stu-id="9bba4-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="9bba4-149">**inicio de sesión único en Azure AD tooconfigure con RFPIO, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bba4-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bba4-150">En el portal de Azure, en Hola Hola **RFPIO** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9bba4-152">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9bba4-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="9bba4-154">En hello **RFPIO dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="9bba4-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="9bba4-156">a.</span><span class="sxs-lookup"><span data-stu-id="9bba4-156">a.</span></span> <span data-ttu-id="9bba4-157">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="9bba4-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="9bba4-159">b.</span><span class="sxs-lookup"><span data-stu-id="9bba4-159">b.</span></span> <span data-ttu-id="9bba4-160">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="9bba4-161">c.</span><span class="sxs-lookup"><span data-stu-id="9bba4-161">c.</span></span> <span data-ttu-id="9bba4-162">Hola **estado de retransmisión** cuadro de texto escriba un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="9bba4-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="9bba4-163">Póngase en contacto con [equipo de soporte técnico RFPIO](https://www.rfpio.com/contact/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="9bba4-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="9bba4-164">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="9bba4-165">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="9bba4-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="9bba4-167">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="9bba4-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="9bba4-168">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9bba4-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="9bba4-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9bba4-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9bba4-172">En una ventana del explorador web diferente, inicio de sesión toohello **RFPIO** sitio Web como administrador.</span><span class="sxs-lookup"><span data-stu-id="9bba4-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="9bba4-173">Haga clic en el desplegable de esquina izquierda inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bba4-173">Click on hello bottom left corner dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="9bba4-175">Haga clic en hello **configuración de la organización**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-175">Click on hello **Organization Settings**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="9bba4-177">Haga clic en hello **características e integración**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="9bba4-179">Hola **configuración de SSO de SAML** haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="9bba4-181">En esta sección, realice las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="9bba4-181">In this Section perform following actions:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="9bba4-183">a.</span><span class="sxs-lookup"><span data-stu-id="9bba4-183">a.</span></span> <span data-ttu-id="9bba4-184">Copiar el contenido de Hola de hello **XML de metadatos descargado** y péguelo en hello **configuración de identidad** campo.</span><span class="sxs-lookup"><span data-stu-id="9bba4-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="9bba4-185">Hola toocopy contenido de descarga **Metadata XML** Use **el Bloc de notas ++** o adecuada **Editor XML**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="9bba4-186">b.</span><span class="sxs-lookup"><span data-stu-id="9bba4-186">b.</span></span> <span data-ttu-id="9bba4-187">Haga clic en **Validar**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-187">Click **Validate**.</span></span>

    <span data-ttu-id="9bba4-188">c.</span><span class="sxs-lookup"><span data-stu-id="9bba4-188">c.</span></span> <span data-ttu-id="9bba4-189">Después de hacer clic **validar**, voltear **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="9bba4-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="9bba4-190">d.</span><span class="sxs-lookup"><span data-stu-id="9bba4-190">d.</span></span> <span data-ttu-id="9bba4-191">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="9bba4-192">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9bba4-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9bba4-193">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9bba4-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9bba4-194">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9bba4-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9bba4-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bba4-195">Create an Azure AD test user</span></span>
<span data-ttu-id="9bba4-196">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9bba4-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9bba4-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bba4-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bba4-199">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9bba4-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9bba4-201">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9bba4-203">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bba4-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9bba4-205">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9bba4-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9bba4-207">a.</span><span class="sxs-lookup"><span data-stu-id="9bba4-207">a.</span></span> <span data-ttu-id="9bba4-208">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9bba4-209">b.</span><span class="sxs-lookup"><span data-stu-id="9bba4-209">b.</span></span> <span data-ttu-id="9bba4-210">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9bba4-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9bba4-211">c.</span><span class="sxs-lookup"><span data-stu-id="9bba4-211">c.</span></span> <span data-ttu-id="9bba4-212">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9bba4-213">d.</span><span class="sxs-lookup"><span data-stu-id="9bba4-213">d.</span></span> <span data-ttu-id="9bba4-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="9bba4-215">Creación de un usuario de prueba de RFPIO</span><span class="sxs-lookup"><span data-stu-id="9bba4-215">Create a RFPIO test user</span></span>

<span data-ttu-id="9bba4-216">toolog de los usuarios de Azure AD tooenable en tooRFPIO, se les deben aprovisionar en RFPIO.</span><span class="sxs-lookup"><span data-stu-id="9bba4-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="9bba4-217">En caso de hello de RFPIO, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9bba4-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="9bba4-218">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bba4-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bba4-219">Inicie sesión en tooyour sitio RFPIO de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="9bba4-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="9bba4-220">Haga clic en el desplegable de esquina izquierda inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bba4-220">Click on hello bottom left corner dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="9bba4-222">Haga clic en hello **configuración de la organización**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-222">Click on hello **Organization Settings**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="9bba4-224">Haga clic en **TEAM MEMBERS** (MIEMBROS DE EQUIPO).</span><span class="sxs-lookup"><span data-stu-id="9bba4-224">Click **TEAM MEMBERS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="9bba4-226">Haga clic en **ADD MEMBERS** (AGREGAR MIEMBROS).</span><span class="sxs-lookup"><span data-stu-id="9bba4-226">Click on **ADD MEMBERS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="9bba4-228">Hola **agregar nuevos miembros** sección.</span><span class="sxs-lookup"><span data-stu-id="9bba4-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="9bba4-229">Realice las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="9bba4-229">Perform following actions:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="9bba4-231">a.</span><span class="sxs-lookup"><span data-stu-id="9bba4-231">a.</span></span> <span data-ttu-id="9bba4-232">ENTRAR **dirección de correo electrónico** en hello **escriba una dirección de correo por línea** campo.</span><span class="sxs-lookup"><span data-stu-id="9bba4-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="9bba4-233">b.</span><span class="sxs-lookup"><span data-stu-id="9bba4-233">b.</span></span> <span data-ttu-id="9bba4-234">Seleccione **Role** (Role) de acuerdo con sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="9bba4-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="9bba4-235">c.</span><span class="sxs-lookup"><span data-stu-id="9bba4-235">c.</span></span> <span data-ttu-id="9bba4-236">Haga clic en **ADD MEMBERS** (AGREGAR MIEMBROS).</span><span class="sxs-lookup"><span data-stu-id="9bba4-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="9bba4-237">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="9bba4-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9bba4-238">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bba4-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9bba4-239">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="9bba4-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9bba4-241">**tooassign Britta Simon tooRFPIO, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9bba4-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bba4-242">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9bba4-244">En la lista de aplicaciones de hello, seleccione **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-244">In hello applications list, select **RFPIO**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="9bba4-246">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9bba4-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-248">Click **Add** button.</span></span> <span data-ttu-id="9bba4-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9bba4-251">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bba4-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9bba4-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9bba4-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9bba4-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9bba4-254">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="9bba4-254">Test single sign-on</span></span>

<span data-ttu-id="9bba4-255">En esta sección, probará la configuración de inicio de sesión única de Azure AD mediante el uso de hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9bba4-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="9bba4-256">Al hacer clic en hello RFPIO el icono Panel de acceso de hello, deberá obtener la aplicación de RFPIO tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="9bba4-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="9bba4-257">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9bba4-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9bba4-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9bba4-258">Additional resources</span></span>

* [<span data-ttu-id="9bba4-259">Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9bba4-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9bba4-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9bba4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

