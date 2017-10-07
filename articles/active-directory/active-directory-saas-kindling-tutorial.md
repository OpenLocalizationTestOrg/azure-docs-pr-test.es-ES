---
title: "Tutorial: Integración de Azure Active Directory con Kindling | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kindling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="bb077-103">Tutorial: Integración de Azure Active Directory con Kindling</span><span class="sxs-lookup"><span data-stu-id="bb077-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="bb077-104">En este tutorial, aprenderá cómo toointegrate Kindling con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb077-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb077-105">Integración Kindling con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bb077-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb077-106">Puede controlar en Azure AD que tenga acceso tooKindling</span><span class="sxs-lookup"><span data-stu-id="bb077-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="bb077-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKindling (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb077-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb077-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bb077-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb077-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="bb077-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="bb077-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="bb077-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb077-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb077-111">Prerequisites</span></span>

<span data-ttu-id="bb077-112">integración de Azure AD tooconfigure con Kindling, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bb077-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="bb077-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb077-113">An Azure AD subscription</span></span>
- <span data-ttu-id="bb077-114">Una suscripción habilitada para el inicio de sesión único en Kindling</span><span class="sxs-lookup"><span data-stu-id="bb077-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb077-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bb077-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb077-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bb077-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb077-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bb077-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb077-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb077-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb077-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bb077-119">Scenario description</span></span>
<span data-ttu-id="bb077-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bb077-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb077-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bb077-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb077-122">Agregar Kindling desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bb077-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="bb077-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb077-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="bb077-124">Agregar Kindling desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bb077-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="bb077-125">integración de hello tooconfigure de Kindling en Azure AD, necesita tooadd Kindling de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bb077-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb077-126">**tooadd Kindling de galería de hello, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bb077-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb077-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bb077-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb077-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bb077-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb077-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb077-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bb077-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb077-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bb077-134">En el cuadro de búsqueda de hello, escriba **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="bb077-134">In hello search box, type **Kindling**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="bb077-136">En el panel de resultados de hello, seleccione **Kindling**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bb077-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb077-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb077-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb077-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kindling con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bb077-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bb077-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kindling es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb077-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="bb077-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kindling necesidades toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="bb077-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="bb077-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Kindling.</span><span class="sxs-lookup"><span data-stu-id="bb077-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="bb077-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Kindling, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bb077-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb077-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="bb077-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb077-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb077-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb077-146">**[Crear un usuario de prueba Kindling](#creating-a-kindling-test-user)**  -toohave un equivalente de Britta Simon en Kindling decir vinculado representación toohello Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="bb077-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb077-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bb077-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb077-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bb077-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb077-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb077-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb077-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Kindling.</span><span class="sxs-lookup"><span data-stu-id="bb077-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="bb077-151">**tooconfigure inicio de sesión único en Azure AD con Kindling, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bb077-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb077-152">En el portal de Azure, en Hola Hola **Kindling** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bb077-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bb077-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bb077-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="bb077-156">En hello **Kindling dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bb077-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="bb077-158">a.</span><span class="sxs-lookup"><span data-stu-id="bb077-158">a.</span></span> <span data-ttu-id="bb077-159">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="bb077-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="bb077-160">b.</span><span class="sxs-lookup"><span data-stu-id="bb077-160">b.</span></span>  <span data-ttu-id="bb077-161">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="bb077-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb077-162">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="bb077-162">These values are not hello real.</span></span> <span data-ttu-id="bb077-163">Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador.</span><span class="sxs-lookup"><span data-stu-id="bb077-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="bb077-164">Póngase en contacto con [equipo de soporte técnico de Kindling](mailto:support@kindlingapp.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="bb077-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="bb077-165">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bb077-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="bb077-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bb077-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb077-169">En hello **Kindling configuración** sección, haga clic en **configurar Kindling** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="bb077-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb077-170">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="bb077-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="bb077-172">tooconfigure inicio de sesión único en **Kindling** lado, necesita hello toosend descargado **certificado (Base64)**, **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio**demasiado[equipo de soporte técnico de Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="bb077-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="bb077-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="bb077-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb077-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="bb077-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb077-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb077-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb077-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb077-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb077-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bb077-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bb077-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bb077-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb077-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bb077-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb077-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bb077-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb077-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb077-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb077-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bb077-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb077-188">a.</span><span class="sxs-lookup"><span data-stu-id="bb077-188">a.</span></span> <span data-ttu-id="bb077-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb077-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb077-190">b.</span><span class="sxs-lookup"><span data-stu-id="bb077-190">b.</span></span> <span data-ttu-id="bb077-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bb077-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb077-192">c.</span><span class="sxs-lookup"><span data-stu-id="bb077-192">c.</span></span> <span data-ttu-id="bb077-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bb077-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb077-194">d.</span><span class="sxs-lookup"><span data-stu-id="bb077-194">d.</span></span> <span data-ttu-id="bb077-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bb077-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="bb077-196">Creación de un usuario de prueba de Kindling</span><span class="sxs-lookup"><span data-stu-id="bb077-196">Creating a Kindling test user</span></span>

<span data-ttu-id="bb077-197">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Kindling toocreate.</span><span class="sxs-lookup"><span data-stu-id="bb077-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="bb077-198">Kindling admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="bb077-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="bb077-199">Ya lo ha habilitado en [Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bb077-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="bb077-200">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="bb077-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb077-201">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb077-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb077-202">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKindling.</span><span class="sxs-lookup"><span data-stu-id="bb077-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bb077-204">**tooassign Britta Simon tooKindling, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bb077-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb077-205">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb077-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bb077-207">En la lista de aplicaciones de hello, seleccione **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="bb077-207">In hello applications list, select **Kindling**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="bb077-209">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb077-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bb077-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bb077-211">Click **Add** button.</span></span> <span data-ttu-id="bb077-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bb077-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bb077-214">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb077-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb077-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb077-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb077-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bb077-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb077-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bb077-217">Testing single sign-on</span></span>

<span data-ttu-id="bb077-218">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bb077-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bb077-219">Al hacer clic en icono de Kindling Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Kindling aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb077-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bb077-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bb077-220">Additional resources</span></span>

* [<span data-ttu-id="bb077-221">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb077-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb077-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb077-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

