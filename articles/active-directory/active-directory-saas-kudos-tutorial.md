---
title: "Tutorial: integración de Azure Active Directory con Kudos | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="9d4c5-103">Tutorial: Integración de Azure Active Directory con Kudos</span><span class="sxs-lookup"><span data-stu-id="9d4c5-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="9d4c5-104">En este tutorial, aprenderá cómo toointegrate Kudos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d4c5-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d4c5-105">Integración de Kudos con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9d4c5-106">Puede controlar en Azure AD que tenga acceso tooKudos</span><span class="sxs-lookup"><span data-stu-id="9d4c5-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="9d4c5-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKudos (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d4c5-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d4c5-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9d4c5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9d4c5-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d4c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d4c5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d4c5-110">Prerequisites</span></span>

<span data-ttu-id="9d4c5-111">integración de Azure AD con Kudos tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="9d4c5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d4c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d4c5-113">Una suscripción habilitada para el inicio de sesión único en Kudos</span><span class="sxs-lookup"><span data-stu-id="9d4c5-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d4c5-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d4c5-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d4c5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d4c5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d4c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d4c5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9d4c5-118">Scenario description</span></span>
<span data-ttu-id="9d4c5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d4c5-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d4c5-121">Agregar Kudos desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9d4c5-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="9d4c5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d4c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="9d4c5-123">Agregar Kudos desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9d4c5-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="9d4c5-124">integración de hello tooconfigure de Kudos en Azure AD, deberá tooadd Kudos de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d4c5-125">**tooadd Kudos de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d4c5-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d4c5-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d4c5-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d4c5-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9d4c5-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9d4c5-133">En el cuadro de búsqueda de hello, escriba **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-133">In hello search box, type **Kudos**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="9d4c5-135">En el panel de resultados de hello, seleccione **Kudos**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d4c5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d4c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d4c5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kudos con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9d4c5-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d4c5-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kudos es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="9d4c5-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kudos debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="9d4c5-141">En Kudos, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9d4c5-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Kudos, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9d4c5-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9d4c5-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d4c5-145">**[Crear un usuario de prueba de Kudos](#creating-a-kudos-test-user)**  -toohave un equivalente de Britta Simon en Kudos que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d4c5-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d4c5-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d4c5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d4c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d4c5-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Kudos.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="9d4c5-150">**inicio de sesión único en Azure AD tooconfigure con Kudos, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d4c5-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d4c5-151">En el portal de Azure, en Hola Hola **Kudos** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9d4c5-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="9d4c5-155">En hello **Kudos dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="9d4c5-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="9d4c5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="9d4c5-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-158">This value is not real.</span></span> <span data-ttu-id="9d4c5-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9d4c5-160">Póngase en contacto con [equipo de soporte técnico de cliente de Kudos](http://success.kudosnow.com/home) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="9d4c5-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="9d4c5-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9d4c5-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d4c5-165">En hello **configuración de Kudos** sección, haga clic en **configurar Kudos** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9d4c5-166">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9d4c5-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="9d4c5-168">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Kudos.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="9d4c5-169">En el menú de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="9d4c5-170">![Configuración](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="9d4c5-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="9d4c5-171">Haga clic en **Integrations \> SSO** (Integraciones > SSO).</span><span class="sxs-lookup"><span data-stu-id="9d4c5-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="9d4c5-172">Hola **SSO** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9d4c5-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="9d4c5-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="9d4c5-174">a.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-174">a.</span></span> <span data-ttu-id="9d4c5-175">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="9d4c5-176">b.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-176">b.</span></span> <span data-ttu-id="9d4c5-177">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="9d4c5-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="9d4c5-178">c.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-178">c.</span></span> <span data-ttu-id="9d4c5-179">En **tooURL de cierre de sesión**, pegue el valor de Hola de **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="9d4c5-180">d.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-180">d.</span></span> <span data-ttu-id="9d4c5-181">Hola **la dirección URL de Kudos** cuadro de texto, escriba el nombre de su compañía.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="9d4c5-182">e.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-182">e.</span></span> <span data-ttu-id="9d4c5-183">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9d4c5-184">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9d4c5-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9d4c5-185">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9d4c5-186">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d4c5-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d4c5-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d4c5-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d4c5-188">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9d4c5-190">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d4c5-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d4c5-191">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d4c5-193">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d4c5-195">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d4c5-197">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d4c5-199">a.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-199">a.</span></span> <span data-ttu-id="9d4c5-200">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d4c5-201">b.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-201">b.</span></span> <span data-ttu-id="9d4c5-202">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d4c5-203">c.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-203">c.</span></span> <span data-ttu-id="9d4c5-204">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9d4c5-205">d.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-205">d.</span></span> <span data-ttu-id="9d4c5-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="9d4c5-207">Creación de un usuario de prueba de Kudos</span><span class="sxs-lookup"><span data-stu-id="9d4c5-207">Creating a Kudos test user</span></span>

<span data-ttu-id="9d4c5-208">En orden tooenable toolog de los usuarios de Azure AD en Kudos, se les deben aprovisionar en Kudos.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="9d4c5-209">En caso de hello de Kudos, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="9d4c5-210">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d4c5-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d4c5-211">Inicie sesión en tooyour **Kudos** como administrador.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="9d4c5-212">En el menú de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="9d4c5-213">![Configuración](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="9d4c5-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="9d4c5-214">Haga clic en **Administrador de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="9d4c5-215">Haga clic en hello **usuarios** ficha y, a continuación, haga clic en **agregar un usuario**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="9d4c5-216">![Administración de usuarios](./media/active-directory-saas-kudos-tutorial/ic787809.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="9d4c5-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="9d4c5-217">Hola **agregar un usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9d4c5-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9d4c5-218">![Agregar un usuario](./media/active-directory-saas-kudos-tutorial/ic787810.png "Agregar un usuario")</span><span class="sxs-lookup"><span data-stu-id="9d4c5-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="9d4c5-219">a.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-219">a.</span></span> <span data-ttu-id="9d4c5-220">Hola de tipo **nombre**, **Last Name**, **correo electrónico** y otros detalles de una cuenta válida de Azure Active Directory que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="9d4c5-221">b.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-221">b.</span></span> <span data-ttu-id="9d4c5-222">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="9d4c5-223">Puede usar cualquier otra Kudos usuario cuenta herramienta de creación o las API proporcionadas por Kudos tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9d4c5-224">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d4c5-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9d4c5-225">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKudos.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9d4c5-227">**tooassign Britta Simon tooKudos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d4c5-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d4c5-228">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9d4c5-230">En la lista de aplicaciones de hello, seleccione **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-230">In hello applications list, select **Kudos**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="9d4c5-232">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9d4c5-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-234">Click **Add** button.</span></span> <span data-ttu-id="9d4c5-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9d4c5-237">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9d4c5-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d4c5-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d4c5-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9d4c5-240">Testing single sign-on</span></span>

<span data-ttu-id="9d4c5-241">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9d4c5-242">Al hacer clic en icono de Kudos Hola Hola Panel de acceso, deberá obtener la aplicación de Kudos tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="9d4c5-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="9d4c5-243">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d4c5-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d4c5-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9d4c5-244">Additional resources</span></span>

* [<span data-ttu-id="9d4c5-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d4c5-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d4c5-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d4c5-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

