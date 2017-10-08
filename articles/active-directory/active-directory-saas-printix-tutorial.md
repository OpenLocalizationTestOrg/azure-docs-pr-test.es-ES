---
title: "Tutorial: Integración de Azure Active Directory con Printix | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="c51a9-103">Tutorial: Integración de Azure Active Directory con Printix</span><span class="sxs-lookup"><span data-stu-id="c51a9-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="c51a9-104">En este tutorial, aprenderá cómo toointegrate Printix con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c51a9-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c51a9-105">Integración Printix con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c51a9-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c51a9-106">Puede controlar en Azure AD que tenga acceso tooPrintix</span><span class="sxs-lookup"><span data-stu-id="c51a9-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="c51a9-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPrintix (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51a9-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c51a9-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c51a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c51a9-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c51a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c51a9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c51a9-110">Prerequisites</span></span>

<span data-ttu-id="c51a9-111">integración de Azure AD con Printix tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c51a9-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="c51a9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c51a9-113">Una suscripción habilitada para el inicio de sesión único en Printix</span><span class="sxs-lookup"><span data-stu-id="c51a9-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c51a9-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c51a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c51a9-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c51a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c51a9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c51a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c51a9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c51a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c51a9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c51a9-118">Scenario description</span></span>
<span data-ttu-id="c51a9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c51a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c51a9-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c51a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c51a9-121">Agregar Printix desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c51a9-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="c51a9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="c51a9-123">Agregar Printix desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c51a9-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="c51a9-124">integración de hello tooconfigure de Printix en Azure AD, deberá tooadd Printix de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c51a9-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c51a9-125">**tooadd Printix de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51a9-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51a9-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c51a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c51a9-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c51a9-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c51a9-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c51a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c51a9-133">En el cuadro de búsqueda de hello, escriba **Printix**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-133">In hello search box, type **Printix**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="c51a9-135">En el panel de resultados de hello, seleccione **Printix**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c51a9-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c51a9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c51a9-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Printix con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c51a9-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c51a9-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Printix es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c51a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="c51a9-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Printix debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c51a9-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="c51a9-141">En Printix, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51a9-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c51a9-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Printix, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c51a9-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c51a9-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c51a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c51a9-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c51a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c51a9-145">**[Crear un usuario de prueba Printix](#creating-a-printix-test-user)**  -toohave un equivalente de Britta Simon en Printix que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c51a9-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c51a9-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c51a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c51a9-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c51a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c51a9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c51a9-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Printix.</span><span class="sxs-lookup"><span data-stu-id="c51a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="c51a9-150">**inicio de sesión único en Azure AD tooconfigure con Printix, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51a9-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51a9-151">En el portal de Azure, en Hola Hola **Printix** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c51a9-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c51a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="c51a9-155">En hello **Printix dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c51a9-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="c51a9-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="c51a9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c51a9-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="c51a9-158">hello value is not real.</span></span> <span data-ttu-id="c51a9-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="c51a9-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c51a9-160">Póngase en contacto con [equipo de soporte técnico de Printix cliente](mailto:support@printix.net) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="c51a9-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="c51a9-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c51a9-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="c51a9-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c51a9-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c51a9-165">Inicio de sesión tooyour Printix inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="c51a9-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="c51a9-166">En el menú de hello en la parte superior de hello, haga clic en el icono de hello en la esquina superior derecha de Hola y seleccione "**autenticación**".</span><span class="sxs-lookup"><span data-stu-id="c51a9-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="c51a9-168">En hello **el programa de instalación** ficha, seleccione **autenticación de habilitar Azure/Office 365**</span><span class="sxs-lookup"><span data-stu-id="c51a9-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="c51a9-170">En hello **Azure** ficha, cuadro de texto de entrada federación metadatos URL toohello de "**documento de metadatos de federación**".</span><span class="sxs-lookup"><span data-stu-id="c51a9-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="c51a9-171">Adjuntar archivo de xml de metadatos de Hola que descargó desde Azure AD demasiado[equipo de soporte técnico de Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="c51a9-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="c51a9-172">A continuación, se cargue el archivo xml de hello y proporcionar una dirección URL de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="c51a9-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="c51a9-174">Haga clic en hello "**probar**"y haga clic en"**Aceptar**" botón si la prueba de hello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="c51a9-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="c51a9-175">Página de Azure active directory mostrará tras hacer clic en hello **probar** botón.</span><span class="sxs-lookup"><span data-stu-id="c51a9-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="c51a9-176">"prueba de hello fue correcta" aquí significa que después de escribir las credenciales de hello de la cuenta de prueba de Azure que mostrará un mensaje de "configuración probado Aceptar". A continuación, haga clic en hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="c51a9-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="c51a9-178">Haga clic en hello **guardar** situado en "**autenticación**" página.</span><span class="sxs-lookup"><span data-stu-id="c51a9-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="c51a9-179">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c51a9-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c51a9-180">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c51a9-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c51a9-181">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c51a9-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c51a9-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51a9-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="c51a9-183">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c51a9-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c51a9-185">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51a9-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51a9-186">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c51a9-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c51a9-188">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c51a9-190">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51a9-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c51a9-192">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c51a9-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c51a9-194">a.</span><span class="sxs-lookup"><span data-stu-id="c51a9-194">a.</span></span> <span data-ttu-id="c51a9-195">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c51a9-196">b.</span><span class="sxs-lookup"><span data-stu-id="c51a9-196">b.</span></span> <span data-ttu-id="c51a9-197">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c51a9-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c51a9-198">c.</span><span class="sxs-lookup"><span data-stu-id="c51a9-198">c.</span></span> <span data-ttu-id="c51a9-199">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c51a9-200">d.</span><span class="sxs-lookup"><span data-stu-id="c51a9-200">d.</span></span> <span data-ttu-id="c51a9-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="c51a9-202">Creación de un usuario de prueba de Printix</span><span class="sxs-lookup"><span data-stu-id="c51a9-202">Creating a Printix test user</span></span>

<span data-ttu-id="c51a9-203">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Printix toocreate.</span><span class="sxs-lookup"><span data-stu-id="c51a9-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="c51a9-204">Printix admite el aprovisionamiento just-in-time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c51a9-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c51a9-205">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="c51a9-205">There is no action item for you in this section.</span></span> <span data-ttu-id="c51a9-206">Se crea un nuevo usuario durante un tooaccess intento Printix si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="c51a9-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="c51a9-207">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="c51a9-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c51a9-208">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51a9-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c51a9-209">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPrintix.</span><span class="sxs-lookup"><span data-stu-id="c51a9-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c51a9-211">**tooassign Britta Simon tooPrintix, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51a9-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51a9-212">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c51a9-214">En la lista de aplicaciones de hello, seleccione **Printix**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-214">In hello applications list, select **Printix**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="c51a9-216">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c51a9-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-218">Click **Add** button.</span></span> <span data-ttu-id="c51a9-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c51a9-221">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51a9-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c51a9-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c51a9-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c51a9-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c51a9-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c51a9-224">Testing single sign-on</span></span>

<span data-ttu-id="c51a9-225">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c51a9-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c51a9-226">Al hacer clic en icono de Printix Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Printix aplicación.</span><span class="sxs-lookup"><span data-stu-id="c51a9-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c51a9-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c51a9-227">Additional resources</span></span>

* [<span data-ttu-id="c51a9-228">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c51a9-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c51a9-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c51a9-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

