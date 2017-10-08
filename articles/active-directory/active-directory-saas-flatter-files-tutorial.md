---
title: "Tutorial: integración de Azure Active Directory con Flatter Files | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y los archivos más plana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="f6540-103">Tutorial: integración de Azure Active Directory con Flatter Files</span><span class="sxs-lookup"><span data-stu-id="f6540-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="f6540-104">En este tutorial, aprenderá cómo toointegrate archivos más plana con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6540-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6540-105">Integración de archivos más plana con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f6540-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6540-106">Puede controlar en Azure AD que tenga acceso a archivos tooFlatter</span><span class="sxs-lookup"><span data-stu-id="f6540-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="f6540-107">Puede habilitar la tooautomatically a los usuarios obtener los archivos de tooFlatter ha iniciado sesión (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6540-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6540-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f6540-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f6540-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6540-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6540-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f6540-110">Prerequisites</span></span>

<span data-ttu-id="f6540-111">tooconfigure integración de Azure AD con archivos más plana, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f6540-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="f6540-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6540-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6540-113">Una suscripción habilitada para el inicio de sesión único en Flatter Files</span><span class="sxs-lookup"><span data-stu-id="f6540-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6540-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f6540-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6540-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f6540-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6540-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f6540-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6540-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6540-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6540-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f6540-118">Scenario description</span></span>
<span data-ttu-id="f6540-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f6540-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6540-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="f6540-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6540-121">Agregar archivos más plana de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f6540-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="f6540-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6540-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="f6540-123">Agregar archivos más plana de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f6540-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="f6540-124">integración de hello tooconfigure de archivos más plana en Azure AD, deberá tooadd archivos más plana de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f6540-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6540-125">**tooadd archivos más plana de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f6540-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6540-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f6540-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6540-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f6540-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6540-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f6540-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f6540-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f6540-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f6540-133">En el cuadro de búsqueda de hello, escriba **archivos más plana**.</span><span class="sxs-lookup"><span data-stu-id="f6540-133">In hello search box, type **Flatter Files**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="f6540-135">En el panel de resultados de hello, seleccione **archivos más plana**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6540-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6540-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6540-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6540-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Flatter Files con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f6540-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6540-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en archivos más plana es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6540-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="f6540-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en archivos más plana debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="f6540-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="f6540-141">En los archivos más plana, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6540-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f6540-142">tooconfigure y prueba de inicio de sesión único en Azure AD con archivos más plana, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f6540-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6540-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="f6540-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6540-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6540-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6540-145">**[Crear un usuario de prueba de archivos más plana](#creating-a-flatter-files-test-user)**  -toohave un equivalente de Britta Simon en archivos más plana que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="f6540-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6540-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f6540-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6540-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f6540-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6540-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6540-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6540-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de archivos más plana.</span><span class="sxs-lookup"><span data-stu-id="f6540-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="f6540-150">**inicio de sesión único en tooconfigure Azure AD con los archivos más plana, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f6540-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6540-151">En el portal de Azure, en Hola Hola **archivos más plana** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f6540-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f6540-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f6540-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="f6540-155">En hello **más plana de archivos de dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="f6540-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="f6540-157">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f6540-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="f6540-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f6540-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6540-161">En hello **más plana de archivos de configuración** sección, haga clic en **configurar archivos más plana** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="f6540-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f6540-162">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="f6540-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="f6540-164">Inicio de sesión tooyour aplicación más plana archivos como administrador.</span><span class="sxs-lookup"><span data-stu-id="f6540-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="f6540-165">Haga clic en **PANEL**.</span><span class="sxs-lookup"><span data-stu-id="f6540-165">Click **DASHBOARD**.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="f6540-167">Haga clic en **configuración**y, a continuación, realizar Hola seguir pasos de hello **empresa** ficha:</span><span class="sxs-lookup"><span data-stu-id="f6540-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="f6540-169">a.</span><span class="sxs-lookup"><span data-stu-id="f6540-169">a.</span></span> <span data-ttu-id="f6540-170">Seleccione **Usar SAML 2.0 para autenticación**.</span><span class="sxs-lookup"><span data-stu-id="f6540-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="f6540-171">b.</span><span class="sxs-lookup"><span data-stu-id="f6540-171">b.</span></span> <span data-ttu-id="f6540-172">Haga clic en **Configurar SAML**.</span><span class="sxs-lookup"><span data-stu-id="f6540-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="f6540-173">En hello **configuración de SAML** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f6540-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="f6540-175">a.</span><span class="sxs-lookup"><span data-stu-id="f6540-175">a.</span></span> <span data-ttu-id="f6540-176">Hola **dominio** cuadro de texto, escriba el dominio registrado.</span><span class="sxs-lookup"><span data-stu-id="f6540-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="f6540-177">Si no dispone de un dominio registrado, póngase en contacto con el equipo de soporte técnico de Flatter Files a través de [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="f6540-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="f6540-178">b.</span><span class="sxs-lookup"><span data-stu-id="f6540-178">b.</span></span> <span data-ttu-id="f6540-179">En **dirección URL del proveedor de identidad** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que copiaste forman el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6540-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="f6540-180">c.</span><span class="sxs-lookup"><span data-stu-id="f6540-180">c.</span></span>  <span data-ttu-id="f6540-181">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="f6540-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="f6540-182">d.</span><span class="sxs-lookup"><span data-stu-id="f6540-182">d.</span></span> <span data-ttu-id="f6540-183">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="f6540-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="f6540-184">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="f6540-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f6540-185">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="f6540-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f6540-186">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6540-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6540-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6540-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6540-188">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f6540-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f6540-190">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f6540-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6540-191">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f6540-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6540-193">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f6540-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6540-195">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6540-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6540-197">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="f6540-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6540-199">a.</span><span class="sxs-lookup"><span data-stu-id="f6540-199">a.</span></span> <span data-ttu-id="f6540-200">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6540-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6540-201">b.</span><span class="sxs-lookup"><span data-stu-id="f6540-201">b.</span></span> <span data-ttu-id="f6540-202">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6540-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6540-203">c.</span><span class="sxs-lookup"><span data-stu-id="f6540-203">c.</span></span> <span data-ttu-id="f6540-204">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f6540-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6540-205">d.</span><span class="sxs-lookup"><span data-stu-id="f6540-205">d.</span></span> <span data-ttu-id="f6540-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f6540-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="f6540-207">Creación de un usuario de prueba de Flatter Files</span><span class="sxs-lookup"><span data-stu-id="f6540-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="f6540-208">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en archivos más plana.</span><span class="sxs-lookup"><span data-stu-id="f6540-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="f6540-209">**toocreate un usuario llamado Britta Simon en archivos más plana, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f6540-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6540-210">Inicio de sesión tooyour **archivos más plana** como administrador.</span><span class="sxs-lookup"><span data-stu-id="f6540-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="f6540-211">En el panel de navegación de Hola Hola izquierda, haga clic en **configuración**y, a continuación, haga clic en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="f6540-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Creación de un usuario de Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="f6540-213">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="f6540-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="f6540-214">En hello **Agregar usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f6540-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Creación de un usuario de Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="f6540-216">a.</span><span class="sxs-lookup"><span data-stu-id="f6540-216">a.</span></span> <span data-ttu-id="f6540-217">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="f6540-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="f6540-218">b.</span><span class="sxs-lookup"><span data-stu-id="f6540-218">b.</span></span> <span data-ttu-id="f6540-219">Hola **Last Name** cuadro de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f6540-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="f6540-220">c.</span><span class="sxs-lookup"><span data-stu-id="f6540-220">c.</span></span> <span data-ttu-id="f6540-221">Hola **dirección de correo electrónico** cuadro de texto, escriba la dirección de correo electrónico de Bárbara Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6540-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="f6540-222">d.</span><span class="sxs-lookup"><span data-stu-id="f6540-222">d.</span></span> <span data-ttu-id="f6540-223">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="f6540-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6540-224">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6540-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6540-225">En esta sección, se habilita las Britta Simon toouse Azure inicio de sesión único mediante la concesión de acceso a archivos de tooFlatter.</span><span class="sxs-lookup"><span data-stu-id="f6540-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f6540-227">**tooassign Britta Simon tooFlatter archivos, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f6540-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6540-228">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f6540-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f6540-230">En la lista de aplicaciones de hello, seleccione **archivos más plana**.</span><span class="sxs-lookup"><span data-stu-id="f6540-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="f6540-232">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f6540-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f6540-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f6540-234">Click **Add** button.</span></span> <span data-ttu-id="f6540-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f6540-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f6540-237">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6540-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6540-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f6540-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6540-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f6540-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6540-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f6540-240">Testing single sign-on</span></span>

<span data-ttu-id="f6540-241">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f6540-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f6540-242">Al hacer clic en hello archivos más plana disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación archivos más plana.</span><span class="sxs-lookup"><span data-stu-id="f6540-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="f6540-243">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f6540-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6540-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f6540-244">Additional resources</span></span>

* [<span data-ttu-id="f6540-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6540-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6540-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6540-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

