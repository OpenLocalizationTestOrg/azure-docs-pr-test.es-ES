---
title: "Tutorial: Integración de Azure Active Directory con Promapp | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="5d0f0-103">Tutorial: Integración de Azure Active Directory con Promapp</span><span class="sxs-lookup"><span data-stu-id="5d0f0-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="5d0f0-104">En este tutorial, aprenderá cómo toointegrate Promapp con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d0f0-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d0f0-105">Integración Promapp con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d0f0-106">Puede controlar en Azure AD que tenga acceso tooPromapp</span><span class="sxs-lookup"><span data-stu-id="5d0f0-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="5d0f0-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPromapp (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d0f0-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d0f0-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5d0f0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5d0f0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d0f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d0f0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5d0f0-110">Prerequisites</span></span>

<span data-ttu-id="5d0f0-111">integración de Azure AD con Promapp tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="5d0f0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d0f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d0f0-113">Una suscripción habilitada para el inicio de sesión único en Promapp</span><span class="sxs-lookup"><span data-stu-id="5d0f0-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d0f0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d0f0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d0f0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d0f0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d0f0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d0f0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5d0f0-118">Scenario description</span></span>
<span data-ttu-id="5d0f0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d0f0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d0f0-121">Agregar Promapp desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5d0f0-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="5d0f0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d0f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="5d0f0-123">Agregar Promapp desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5d0f0-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="5d0f0-124">integración de hello tooconfigure de Promapp en Azure AD, deberá tooadd Promapp de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d0f0-125">**tooadd Promapp de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d0f0-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d0f0-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d0f0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d0f0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5d0f0-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5d0f0-133">En el cuadro de búsqueda de hello, escriba **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-133">In hello search box, type **Promapp**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="5d0f0-135">En el panel de resultados de hello, seleccione **Promapp**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d0f0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d0f0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d0f0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Promapp con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5d0f0-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d0f0-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Promapp es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="5d0f0-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Promapp debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="5d0f0-141">En Promapp, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d0f0-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Promapp, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d0f0-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d0f0-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d0f0-145">**[Crear un usuario de prueba Promapp](#creating-a-promapp-test-user)**  -toohave un equivalente de Britta Simon en Promapp que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d0f0-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d0f0-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d0f0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d0f0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d0f0-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Promapp.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="5d0f0-150">**inicio de sesión único en Azure AD tooconfigure con Promapp, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d0f0-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d0f0-151">En el portal de Azure, en Hola Hola **Promapp** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5d0f0-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="5d0f0-155">En hello **Promapp dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="5d0f0-157">a.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-157">a.</span></span> <span data-ttu-id="5d0f0-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="5d0f0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="5d0f0-159">b.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-159">b.</span></span> <span data-ttu-id="5d0f0-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="5d0f0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d0f0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-161">These values are not real.</span></span> <span data-ttu-id="5d0f0-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5d0f0-163">Póngase en contacto con [equipo de soporte técnico de cliente de Promapp](https://www.promapp.com/about-us/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="5d0f0-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="5d0f0-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5d0f0-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5d0f0-168">En hello **Promapp configuración** sección, haga clic en **configurar Promapp** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5d0f0-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="5d0f0-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="5d0f0-171">Sitio de empresa de Promapp tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="5d0f0-172">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][12]

9. <span data-ttu-id="5d0f0-174">Haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-174">Click **Configure**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][13]

10. <span data-ttu-id="5d0f0-176">En hello **seguridad** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Inicio de sesión único de Azure AD ][14]
    
    <span data-ttu-id="5d0f0-178">a.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-178">a.</span></span> <span data-ttu-id="5d0f0-179">Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **dirección URL de inicio de sesión SSO** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="5d0f0-180">b.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-180">b.</span></span> <span data-ttu-id="5d0f0-181">En **SSO - Single Sign-on Mode** (SSO - Modo de inicio de sesión único), seleccione **Optional** (Opcional) y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="5d0f0-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="5d0f0-182">c.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-182">c.</span></span> <span data-ttu-id="5d0f0-183">Abra Hola descargado el certificado en el Bloc de notas, copiar el contenido de certificado de hello sin Hola primera línea (---BEGIN CERTIFICATE---) y la última línea de hello (---END CERTIFICATE---), péguela en hello **certificado x.509 de SSO** cuadro de texto y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="5d0f0-184">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="5d0f0-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d0f0-185">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d0f0-186">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d0f0-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d0f0-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d0f0-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d0f0-188">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5d0f0-190">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d0f0-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d0f0-191">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d0f0-193">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d0f0-195">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d0f0-197">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5d0f0-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d0f0-199">a.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-199">a.</span></span> <span data-ttu-id="5d0f0-200">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d0f0-201">b.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-201">b.</span></span> <span data-ttu-id="5d0f0-202">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d0f0-203">c.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-203">c.</span></span> <span data-ttu-id="5d0f0-204">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5d0f0-205">d.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-205">d.</span></span> <span data-ttu-id="5d0f0-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="5d0f0-207">Creación de un usuario de prueba de Promapp</span><span class="sxs-lookup"><span data-stu-id="5d0f0-207">Creating a Promapp test user</span></span>

<span data-ttu-id="5d0f0-208">Hola Promapp aplicación admite Just-in-Time de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="5d0f0-209">Esto significa que, una cuenta de usuario se crea automáticamente si es necesario durante una aplicación de Hola de tooaccess intento con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5d0f0-210">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d0f0-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5d0f0-211">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPromapp.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5d0f0-213">**tooassign Britta Simon tooPromapp, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5d0f0-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d0f0-214">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5d0f0-216">En la lista de aplicaciones de hello, seleccione **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-216">In hello applications list, select **Promapp**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="5d0f0-218">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5d0f0-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-220">Click **Add** button.</span></span> <span data-ttu-id="5d0f0-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5d0f0-223">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d0f0-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d0f0-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d0f0-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5d0f0-226">Testing single sign-on</span></span>

<span data-ttu-id="5d0f0-227">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5d0f0-228">Al hacer clic en icono de Promapp Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Promapp aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d0f0-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d0f0-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5d0f0-229">Additional resources</span></span>

* [<span data-ttu-id="5d0f0-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d0f0-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d0f0-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5d0f0-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

