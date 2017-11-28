---
title: "Tutorial: Integración de Azure Active Directory con RunMyProcess | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="9e7cc-103">Tutorial: Integración de Azure Active Directory con RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="9e7cc-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="9e7cc-104">En este tutorial, aprenderá cómo toointegrate RunMyProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e7cc-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e7cc-105">Integración de RunMyProcess con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9e7cc-106">Puede controlar en Azure AD que tenga acceso tooRunMyProcess</span><span class="sxs-lookup"><span data-stu-id="9e7cc-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="9e7cc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRunMyProcess (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7cc-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e7cc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9e7cc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9e7cc-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e7cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e7cc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9e7cc-110">Prerequisites</span></span>

<span data-ttu-id="9e7cc-111">integración de Azure AD con RunMyProcess tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="9e7cc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e7cc-113">Una suscripción habilitada para inicio de sesión único en RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="9e7cc-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e7cc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e7cc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e7cc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e7cc-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e7cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e7cc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9e7cc-118">Scenario description</span></span>
<span data-ttu-id="9e7cc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e7cc-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e7cc-121">Agregar RunMyProcess desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9e7cc-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="9e7cc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="9e7cc-123">Agregar RunMyProcess desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9e7cc-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="9e7cc-124">integración de hello tooconfigure de RunMyProcess en Azure AD, deberá tooadd RunMyProcess de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9e7cc-125">**tooadd RunMyProcess de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e7cc-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e7cc-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e7cc-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9e7cc-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9e7cc-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9e7cc-133">En el cuadro de búsqueda de hello, escriba **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="9e7cc-135">En el panel de resultados de hello, seleccione **RunMyProcess**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e7cc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e7cc-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con RunMyProcess con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9e7cc-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e7cc-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en RunMyProcess es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="9e7cc-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en RunMyProcess debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="9e7cc-141">En RunMyProcess, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9e7cc-142">tooconfigure y prueba de inicio de sesión único en Azure AD con RunMyProcess, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9e7cc-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9e7cc-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e7cc-145">**[Crear un usuario de prueba de RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave un equivalente de Britta Simon en RunMyProcess que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e7cc-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e7cc-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e7cc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e7cc-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="9e7cc-150">**inicio de sesión único en Azure AD tooconfigure con RunMyProcess, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e7cc-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e7cc-151">En el portal de Azure, en Hola Hola **RunMyProcess** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9e7cc-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="9e7cc-155">En hello **RunMyProcess dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="9e7cc-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="9e7cc-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e7cc-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-158">hello value is not real.</span></span> <span data-ttu-id="9e7cc-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9e7cc-160">Póngase en contacto con [equipo de soporte técnico de RunMyProcess cliente](mailto:support@runmyprocess.com) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="9e7cc-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="9e7cc-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9e7cc-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e7cc-165">En hello **configuración de RunMyProcess** sección, haga clic en **configurar RunMyProcess** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9e7cc-166">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9e7cc-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="9e7cc-168">En una ventana del explorador web diferente, inquilino de RunMyProcess tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="9e7cc-169">En el panel de navegación izquierdo, haga clic en **Account** (Cuenta) y seleccione **Configuration** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="9e7cc-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="9e7cc-171">Vaya demasiado**método de autenticación** sección y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="9e7cc-173">a.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-173">a.</span></span> <span data-ttu-id="9e7cc-174">En **Método**, seleccione **SSO con Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="9e7cc-175">b.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-175">b.</span></span> <span data-ttu-id="9e7cc-176">Hola **redireccionamiento SSO** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9e7cc-177">c.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-177">c.</span></span> <span data-ttu-id="9e7cc-178">Hola **redireccionamiento de cierre de sesión** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9e7cc-179">d.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-179">d.</span></span> <span data-ttu-id="9e7cc-180">Hola **formato de Id. de nombre** cuadro de texto, valor de tipo hello de **formato de nombre de identificador** como **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="9e7cc-181">e.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-181">e.</span></span> <span data-ttu-id="9e7cc-182">Copiar el contenido de Hola Hola descargado del archivo de certificado y, a continuación, péguelo en hello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="9e7cc-183">f.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-183">f.</span></span> <span data-ttu-id="9e7cc-184">Haga clic en el icono **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="9e7cc-185">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9e7cc-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9e7cc-186">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9e7cc-187">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e7cc-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e7cc-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7cc-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e7cc-189">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9e7cc-191">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e7cc-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e7cc-192">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e7cc-194">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e7cc-196">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e7cc-198">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e7cc-200">a.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-200">a.</span></span> <span data-ttu-id="9e7cc-201">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e7cc-202">b.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-202">b.</span></span> <span data-ttu-id="9e7cc-203">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e7cc-204">c.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-204">c.</span></span> <span data-ttu-id="9e7cc-205">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9e7cc-206">d.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-206">d.</span></span> <span data-ttu-id="9e7cc-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="9e7cc-208">Creación de un usuario de prueba de RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="9e7cc-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="9e7cc-209">En orden tooenable toolog de los usuarios de Azure AD en tooRunMyProcess, se les deben aprovisionar en RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="9e7cc-210">En caso de hello de RunMyProcess, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="9e7cc-211">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e7cc-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e7cc-212">Inicie sesión en tooyour sitio de empresa de RunMyProcess como administrador.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="9e7cc-213">Haga clic en **Account** (Cuenta) y seleccione **Users** (Usuarios) en el panel de navegación izquierdo y, a continuación, haga clic en **New User** (Usuario nuevo).</span><span class="sxs-lookup"><span data-stu-id="9e7cc-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="9e7cc-214">![Nuevo usuario](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="9e7cc-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="9e7cc-215">Hola **configuración de usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9e7cc-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9e7cc-216">![Perfil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="9e7cc-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="9e7cc-217">a.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-217">a.</span></span> <span data-ttu-id="9e7cc-218">Hola de tipo **nombre** y **correo electrónico** de un Azure válida cuadros de texto relacionados con la cuenta de AD que quiera tooprovision en Hola.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="9e7cc-219">b.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-219">b.</span></span> <span data-ttu-id="9e7cc-220">Seleccione un **lenguaje IDE**, un **lenguaje** y un **perfil**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="9e7cc-221">c.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-221">c.</span></span> <span data-ttu-id="9e7cc-222">Seleccione **toome de correo electrónico de creación de cuenta de envío**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="9e7cc-223">d.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-223">d.</span></span> <span data-ttu-id="9e7cc-224">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9e7cc-225">Puede usar cualquier otra RunMyProcess usuario cuenta herramienta de creación o las API proporcionadas por RunMyProcess tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9e7cc-226">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7cc-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9e7cc-227">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9e7cc-229">**tooassign Britta Simon tooRunMyProcess, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e7cc-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e7cc-230">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9e7cc-232">En la lista de aplicaciones de hello, seleccione **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="9e7cc-234">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9e7cc-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-236">Click **Add** button.</span></span> <span data-ttu-id="9e7cc-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9e7cc-239">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9e7cc-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e7cc-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e7cc-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9e7cc-242">Testing single sign-on</span></span>

<span data-ttu-id="9e7cc-243">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="9e7cc-244">Al hacer clic en hello RunMyProcess disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour RunMyProcess aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e7cc-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e7cc-245">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9e7cc-245">Additional resources</span></span>

* [<span data-ttu-id="9e7cc-246">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e7cc-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e7cc-247">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e7cc-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

