---
title: "Tutorial: Integración de Azure Active Directory con Aravo | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Aravo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 8f1336fa307fa9e8d625440a573d9f9d79dd820b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a><span data-ttu-id="14b14-103">Tutorial: Integración de Azure Active Directory con Aravo</span><span class="sxs-lookup"><span data-stu-id="14b14-103">Tutorial: Azure Active Directory integration with Aravo</span></span>

<span data-ttu-id="14b14-104">En este tutorial, aprenderá cómo toointegrate Aravo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14b14-104">In this tutorial, you learn how toointegrate Aravo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14b14-105">Integración Aravo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="14b14-105">Integrating Aravo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="14b14-106">Puede controlar en Azure AD que tenga acceso tooAravo</span><span class="sxs-lookup"><span data-stu-id="14b14-106">You can control in Azure AD who has access tooAravo</span></span>
- <span data-ttu-id="14b14-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAravo (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14b14-107">You can enable your users tooautomatically get signed-on tooAravo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14b14-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="14b14-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="14b14-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14b14-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14b14-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="14b14-110">Prerequisites</span></span>

<span data-ttu-id="14b14-111">integración de Azure AD con Aravo tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="14b14-111">tooconfigure Azure AD integration with Aravo, you need hello following items:</span></span>

- <span data-ttu-id="14b14-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14b14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14b14-113">Una suscripción habilitada para inicio de sesión único en Aravo</span><span class="sxs-lookup"><span data-stu-id="14b14-113">An Aravo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14b14-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="14b14-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14b14-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="14b14-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14b14-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="14b14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14b14-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14b14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14b14-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="14b14-118">Scenario description</span></span>
<span data-ttu-id="14b14-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="14b14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14b14-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="14b14-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14b14-121">Agregar Aravo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="14b14-121">Adding Aravo from hello gallery</span></span>
2. <span data-ttu-id="14b14-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14b14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aravo-from-hello-gallery"></a><span data-ttu-id="14b14-123">Agregar Aravo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="14b14-123">Adding Aravo from hello gallery</span></span>
<span data-ttu-id="14b14-124">integración de hello tooconfigure de Aravo en Azure AD, deberá tooadd Aravo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="14b14-124">tooconfigure hello integration of Aravo into Azure AD, you need tooadd Aravo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="14b14-125">**tooadd Aravo de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14b14-125">**tooadd Aravo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="14b14-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="14b14-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="14b14-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="14b14-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="14b14-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="14b14-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="14b14-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="14b14-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="14b14-133">En el cuadro de búsqueda de hello, escriba **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="14b14-133">In hello search box, type **Aravo**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_search.png)

5. <span data-ttu-id="14b14-135">En el panel de resultados de hello, seleccione **Aravo**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="14b14-135">In hello results panel, select **Aravo**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="14b14-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14b14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="14b14-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Aravo con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="14b14-138">In this section, you configure and test Azure AD single sign-on with Aravo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="14b14-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Aravo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14b14-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aravo is tooa user in Azure AD.</span></span> <span data-ttu-id="14b14-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Aravo debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="14b14-140">In other words, a link relationship between an Azure AD user and hello related user in Aravo needs toobe established.</span></span>

<span data-ttu-id="14b14-141">En Aravo, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="14b14-141">In Aravo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="14b14-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Aravo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="14b14-142">tooconfigure and test Azure AD single sign-on with Aravo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="14b14-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="14b14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="14b14-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14b14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14b14-145">**[Creación de un usuario de prueba Aravo](#creating-an-aravo-test-user)**  -toohave un equivalente de Britta Simon en Aravo que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="14b14-145">**[Creating an Aravo test user](#creating-an-aravo-test-user)** - toohave a counterpart of Britta Simon in Aravo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="14b14-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="14b14-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14b14-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="14b14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="14b14-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14b14-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="14b14-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Aravo.</span><span class="sxs-lookup"><span data-stu-id="14b14-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aravo application.</span></span>

<span data-ttu-id="14b14-150">**inicio de sesión único en Azure AD tooconfigure con Aravo, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14b14-150">**tooconfigure Azure AD single sign-on with Aravo, perform hello following steps:**</span></span>

1. <span data-ttu-id="14b14-151">En el portal de Azure, en Hola Hola **Aravo** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="14b14-151">In hello Azure portal, on hello **Aravo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="14b14-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="14b14-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_samlbase.png)

3. <span data-ttu-id="14b14-155">En hello **Aravo dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="14b14-155">On hello **Aravo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_url.png)

    <span data-ttu-id="14b14-157">a.</span><span class="sxs-lookup"><span data-stu-id="14b14-157">a.</span></span> <span data-ttu-id="14b14-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.aravo.com`</span><span class="sxs-lookup"><span data-stu-id="14b14-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aravo.com`</span></span>

    <span data-ttu-id="14b14-159">b.</span><span class="sxs-lookup"><span data-stu-id="14b14-159">b.</span></span> <span data-ttu-id="14b14-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.aravo.com/aems/login.do`</span><span class="sxs-lookup"><span data-stu-id="14b14-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.aravo.com/aems/login.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14b14-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="14b14-161">These values are not real.</span></span> <span data-ttu-id="14b14-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="14b14-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="14b14-163">Póngase en contacto con [equipo de soporte técnico de Aravo](http://www.aravo.com/about-us/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="14b14-163">Contact [Aravo support team](http://www.aravo.com/about-us/contact/) tooget these values.</span></span>
 
4. <span data-ttu-id="14b14-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="14b14-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_certificate.png) 

5. <span data-ttu-id="14b14-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="14b14-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aravo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="14b14-168">En hello **Aravo configuración** sección, haga clic en **configurar Aravo** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="14b14-168">On hello **Aravo Configuration** section, click **Configure Aravo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="14b14-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="14b14-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_configure.png) 

7. <span data-ttu-id="14b14-171">tooconfigure inicio de sesión único en **Aravo** lado, necesita hello toosend descargado **certificado (Base64)**, **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio**demasiado[equipo de soporte técnico de Aravo](http://www.aravo.com/about-us/contact/).</span><span class="sxs-lookup"><span data-stu-id="14b14-171">tooconfigure single sign-on on **Aravo** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Aravo support team](http://www.aravo.com/about-us/contact/).</span></span> 


> [!TIP]
> <span data-ttu-id="14b14-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="14b14-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="14b14-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="14b14-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="14b14-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14b14-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="14b14-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="14b14-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="14b14-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="14b14-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="14b14-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14b14-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="14b14-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="14b14-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14b14-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="14b14-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14b14-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="14b14-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14b14-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="14b14-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14b14-187">a.</span><span class="sxs-lookup"><span data-stu-id="14b14-187">a.</span></span> <span data-ttu-id="14b14-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14b14-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14b14-189">b.</span><span class="sxs-lookup"><span data-stu-id="14b14-189">b.</span></span> <span data-ttu-id="14b14-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="14b14-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14b14-191">c.</span><span class="sxs-lookup"><span data-stu-id="14b14-191">c.</span></span> <span data-ttu-id="14b14-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="14b14-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="14b14-193">d.</span><span class="sxs-lookup"><span data-stu-id="14b14-193">d.</span></span> <span data-ttu-id="14b14-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="14b14-194">Click **Create**.</span></span>
 
### <a name="creating-an-aravo-test-user"></a><span data-ttu-id="14b14-195">Creación de un usuario de prueba de Aravo</span><span class="sxs-lookup"><span data-stu-id="14b14-195">Creating an Aravo test user</span></span>

<span data-ttu-id="14b14-196">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Aravo toocreate.</span><span class="sxs-lookup"><span data-stu-id="14b14-196">hello objective of this section is toocreate a user called Britta Simon in Aravo.</span></span> <span data-ttu-id="14b14-197">Trabajar con [equipo de soporte técnico de Aravo](http://www.aravo.com/about-us/contact/) a los usuarios de tooadd Hola Hola Aravo cuenta.</span><span class="sxs-lookup"><span data-stu-id="14b14-197">Work with [Aravo support team](http://www.aravo.com/about-us/contact/) tooadd hello users in hello Aravo account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="14b14-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="14b14-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="14b14-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAravo.</span><span class="sxs-lookup"><span data-stu-id="14b14-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAravo.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="14b14-201">**tooassign Britta Simon tooAravo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="14b14-201">**tooassign Britta Simon tooAravo, perform hello following steps:**</span></span>

1. <span data-ttu-id="14b14-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="14b14-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="14b14-204">En la lista de aplicaciones de hello, seleccione **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="14b14-204">In hello applications list, select **Aravo**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_app.png) 

3. <span data-ttu-id="14b14-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="14b14-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="14b14-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="14b14-208">Click **Add** button.</span></span> <span data-ttu-id="14b14-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="14b14-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="14b14-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="14b14-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="14b14-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="14b14-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14b14-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="14b14-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="14b14-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="14b14-214">Testing single sign-on</span></span>

<span data-ttu-id="14b14-215">objetivo de Hola de esta sección es tootest el inicio de sesión único en Microsoft Azure AD de configuración mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="14b14-215">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="14b14-216">Al hacer clic en icono de Aravo Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Aravo aplicación.</span><span class="sxs-lookup"><span data-stu-id="14b14-216">When you click hello Aravo tile in hello Access Panel, you should get automatically signed-on tooyour Aravo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14b14-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="14b14-217">Additional resources</span></span>

* [<span data-ttu-id="14b14-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14b14-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14b14-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14b14-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_203.png

