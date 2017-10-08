---
title: "Tutorial: Integración de Azure Active Directory con Namely | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y a saber."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="4b63b-103">Tutorial: Integración de Azure Active Directory con Namely</span><span class="sxs-lookup"><span data-stu-id="4b63b-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="4b63b-104">En este tutorial, aprenderá cómo toointegrate a saber con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b63b-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b63b-105">Es decir, integración con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4b63b-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b63b-106">Puede controlar en Azure AD que tenga acceso tooNamely</span><span class="sxs-lookup"><span data-stu-id="4b63b-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="4b63b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNamely (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63b-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b63b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4b63b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4b63b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b63b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b63b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4b63b-110">Prerequisites</span></span>

<span data-ttu-id="4b63b-111">integración de Azure AD tooconfigure con; es decir, se necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4b63b-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="4b63b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b63b-113">Una suscripción habilitada para el inicio de sesión único en Namely</span><span class="sxs-lookup"><span data-stu-id="4b63b-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b63b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4b63b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b63b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4b63b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b63b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4b63b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b63b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b63b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b63b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4b63b-118">Scenario description</span></span>
<span data-ttu-id="4b63b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4b63b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b63b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4b63b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b63b-121">Es decir, agregar desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4b63b-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="4b63b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="4b63b-123">Es decir, agregar desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4b63b-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="4b63b-124">integración de hello tooconfigure de concretamente en Azure AD, deberá tooadd a saber de lista de tooyour de hello Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4b63b-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b63b-125">**tooadd a saber de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b63b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4b63b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b63b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b63b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4b63b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b63b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4b63b-133">En el cuadro de búsqueda de hello, escriba **a saber**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-133">In hello search box, type **Namely**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="4b63b-135">En el panel de resultados de hello, seleccione **a saber**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b63b-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b63b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b63b-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Namely con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4b63b-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b63b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en; es decir es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b63b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="4b63b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en concretamente debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4b63b-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="4b63b-141">En asignar; es decir, el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b63b-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b63b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con; es decir, necesitan hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4b63b-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b63b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4b63b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b63b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b63b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b63b-145">**[Crear un usuario de prueba a saber](#creating-a-namely-test-user)**  -toohave un equivalente de Britta Simon en es decir, es decir vinculado toohello representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4b63b-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b63b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4b63b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b63b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4b63b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b63b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b63b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su aplicación a saber.</span><span class="sxs-lookup"><span data-stu-id="4b63b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="4b63b-150">**inicio de sesión único en Azure AD tooconfigure con; es decir, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b63b-151">En el portal de Azure, en Hola Hola **a saber** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4b63b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4b63b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="4b63b-155">En hello **; es decir, dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4b63b-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="4b63b-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b63b-157">a.</span></span> <span data-ttu-id="4b63b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="4b63b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="4b63b-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b63b-159">b.</span></span> <span data-ttu-id="4b63b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="4b63b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b63b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4b63b-161">These values are not real.</span></span> <span data-ttu-id="4b63b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="4b63b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4b63b-163">Póngase en contacto con [equipo de soporte técnico de cliente a saber](https://www.namely.com/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="4b63b-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="4b63b-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4b63b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="4b63b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4b63b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b63b-168">En hello **a saber configuración** sección, haga clic en **configurar concretamente** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4b63b-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4b63b-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="4b63b-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="4b63b-171">En otra ventana del explorador, inicie sesión en tooyour es decir, el sitio de la compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="4b63b-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="4b63b-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en **empresa**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="4b63b-174">Haga clic en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="4b63b-174">Click hello **Settings** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="4b63b-176">Haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-176">Click **SAML**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="4b63b-178">En hello **configuración SAML** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4b63b-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="4b63b-180">a.</span><span class="sxs-lookup"><span data-stu-id="4b63b-180">a.</span></span> <span data-ttu-id="4b63b-181">Haga clic en **Enable SAML**(Habilitar SAML).</span><span class="sxs-lookup"><span data-stu-id="4b63b-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="4b63b-182">b.</span><span class="sxs-lookup"><span data-stu-id="4b63b-182">b.</span></span> <span data-ttu-id="4b63b-183">Hola **url SSO del proveedor de identidades** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b63b-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4b63b-184">c.</span><span class="sxs-lookup"><span data-stu-id="4b63b-184">c.</span></span> <span data-ttu-id="4b63b-185">Abra el certificado descargado en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **certificado del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4b63b-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="4b63b-186">d.</span><span class="sxs-lookup"><span data-stu-id="4b63b-186">d.</span></span> <span data-ttu-id="4b63b-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4b63b-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4b63b-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b63b-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4b63b-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b63b-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b63b-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b63b-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63b-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b63b-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4b63b-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4b63b-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b63b-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4b63b-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b63b-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b63b-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b63b-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b63b-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4b63b-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b63b-203">a.</span><span class="sxs-lookup"><span data-stu-id="4b63b-203">a.</span></span> <span data-ttu-id="4b63b-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b63b-205">b.</span><span class="sxs-lookup"><span data-stu-id="4b63b-205">b.</span></span> <span data-ttu-id="4b63b-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b63b-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b63b-207">c.</span><span class="sxs-lookup"><span data-stu-id="4b63b-207">c.</span></span> <span data-ttu-id="4b63b-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b63b-209">d.</span><span class="sxs-lookup"><span data-stu-id="4b63b-209">d.</span></span> <span data-ttu-id="4b63b-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="4b63b-211">Creación de un usuario de prueba en Namely</span><span class="sxs-lookup"><span data-stu-id="4b63b-211">Creating a Namely test user</span></span>

<span data-ttu-id="4b63b-212">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon concretamente.</span><span class="sxs-lookup"><span data-stu-id="4b63b-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="4b63b-213">**toocreate un usuario llamado Britta Simon; es decir, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b63b-214">Tooyour inicio de sesión de la compañía a saber sitio como administrador.</span><span class="sxs-lookup"><span data-stu-id="4b63b-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="4b63b-215">En la barra de herramientas de hello en la parte superior de hello, haga clic en **personas**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="4b63b-217">Haga clic en hello **Directory** ficha.</span><span class="sxs-lookup"><span data-stu-id="4b63b-217">Click hello **Directory** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="4b63b-219">Haga clic en **Agregar nueva persona**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-219">Click **Add New Person**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="4b63b-221">En hello **agregar nueva persona** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4b63b-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="4b63b-222">a.</span><span class="sxs-lookup"><span data-stu-id="4b63b-222">a.</span></span> <span data-ttu-id="4b63b-223">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="4b63b-224">b.</span><span class="sxs-lookup"><span data-stu-id="4b63b-224">b.</span></span> <span data-ttu-id="4b63b-225">Hola **apellidos** cuadro de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="4b63b-226">c.</span><span class="sxs-lookup"><span data-stu-id="4b63b-226">c.</span></span> <span data-ttu-id="4b63b-227">Hola **correo electrónico** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b63b-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b63b-228">d.</span><span class="sxs-lookup"><span data-stu-id="4b63b-228">d.</span></span> <span data-ttu-id="4b63b-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b63b-230">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63b-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b63b-231">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNamely.</span><span class="sxs-lookup"><span data-stu-id="4b63b-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4b63b-233">**tooassign Britta Simon tooNamely, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b63b-234">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4b63b-236">En la lista de aplicaciones de hello, seleccione **a saber**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-236">In hello applications list, select **Namely**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="4b63b-238">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4b63b-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-240">Click **Add** button.</span></span> <span data-ttu-id="4b63b-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4b63b-243">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b63b-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b63b-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b63b-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4b63b-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b63b-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4b63b-246">Testing single sign-on</span></span>

<span data-ttu-id="4b63b-247">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4b63b-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b63b-248">Al hacer clic en hello es decir, el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación; es decir</span><span class="sxs-lookup"><span data-stu-id="4b63b-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b63b-249">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4b63b-249">Additional resources</span></span>

* [<span data-ttu-id="4b63b-250">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b63b-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b63b-251">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b63b-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

