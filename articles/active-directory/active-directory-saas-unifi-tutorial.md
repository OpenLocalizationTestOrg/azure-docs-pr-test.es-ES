---
title: "Tutorial: Integración de Azure Active Directory con UNIFI | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="c642b-103">Tutorial: Integración de Azure Active Directory con UNIFI</span><span class="sxs-lookup"><span data-stu-id="c642b-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="c642b-104">En este tutorial, aprenderá cómo toointegrate UNIFI con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c642b-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c642b-105">Integración UNIFI con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c642b-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c642b-106">Puede controlar en Azure AD que tenga acceso tooUNIFI</span><span class="sxs-lookup"><span data-stu-id="c642b-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="c642b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooUNIFI (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c642b-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c642b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c642b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c642b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c642b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c642b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c642b-110">Prerequisites</span></span>

<span data-ttu-id="c642b-111">integración de Azure AD con UNIFI tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c642b-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="c642b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c642b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c642b-113">Una suscripción habilitada para el inicio de sesión único en UNIFI</span><span class="sxs-lookup"><span data-stu-id="c642b-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c642b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c642b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c642b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c642b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c642b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c642b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c642b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c642b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c642b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c642b-118">Scenario description</span></span>
<span data-ttu-id="c642b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c642b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c642b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c642b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c642b-121">Agregar UNIFI desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c642b-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="c642b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c642b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="c642b-123">Agregar UNIFI desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c642b-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="c642b-124">integración de hello tooconfigure de UNIFI en Azure AD, deberá tooadd UNIFI de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c642b-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c642b-125">**tooadd UNIFI de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c642b-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c642b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c642b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c642b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c642b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c642b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c642b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c642b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c642b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c642b-133">En el cuadro de búsqueda de hello, escriba **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="c642b-133">In hello search box, type **UNIFI**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="c642b-135">En el panel de resultados de hello, seleccione **UNIFI**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c642b-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c642b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c642b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c642b-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con UNIFI con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c642b-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c642b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en UNIFI es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c642b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="c642b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en UNIFI debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c642b-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="c642b-141">En UNIFI, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c642b-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c642b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con UNIFI, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c642b-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c642b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c642b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c642b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c642b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c642b-145">**[Usuario de prueba de la creación de un UNIFI](#creating-a-unifi-test-user)**  -toohave un equivalente de Britta Simon en UNIFI que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c642b-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c642b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c642b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c642b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c642b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c642b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c642b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c642b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación UNIFI.</span><span class="sxs-lookup"><span data-stu-id="c642b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="c642b-150">**inicio de sesión único en Azure AD tooconfigure con UNIFI, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c642b-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="c642b-151">En el portal de Azure, en Hola Hola **UNIFI** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c642b-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c642b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c642b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="c642b-155">En hello **UNIFI dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="c642b-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="c642b-157">Hola **identificador** cuadro de texto, valor de tipo hello:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="c642b-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="c642b-158">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="c642b-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="c642b-160">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="c642b-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="c642b-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c642b-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="c642b-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c642b-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c642b-165">En hello **UNIFI configuración** sección, haga clic en **configurar UNIFI** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c642b-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c642b-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c642b-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="c642b-168">En una ventana del explorador web diferente, inicie sesión en tooyour **UNIFI** como administrador.</span><span class="sxs-lookup"><span data-stu-id="c642b-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="c642b-169">Haga clic en hello **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c642b-169">Click on hello **Users**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="c642b-171">Haga clic en hello **Agregar nuevo proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="c642b-171">Click on hello **Add New Identity Provider**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="c642b-173">Hola **Agregar proveedor de identidades** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c642b-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="c642b-175">a.</span><span class="sxs-lookup"><span data-stu-id="c642b-175">a.</span></span> <span data-ttu-id="c642b-176">Hola **nombre de proveedor** cuadro de texto Nombre de Hola de tipo de proveedor de identidades de Hola...</span><span class="sxs-lookup"><span data-stu-id="c642b-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="c642b-177">b.</span><span class="sxs-lookup"><span data-stu-id="c642b-177">b.</span></span> <span data-ttu-id="c642b-178">Hola Hola **dirección URL del proveedor** textbox pegar hello **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c642b-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c642b-179">c.</span><span class="sxs-lookup"><span data-stu-id="c642b-179">c.</span></span> <span data-ttu-id="c642b-180">Hola abierto certificado que ha descargado de hello portal de Azure en el Bloc de notas, quite hello **---BEGIN CERTIFICATE---** y **---END CERTIFICATE---** etiqueta y, a continuación, pegue Hola restantes contenido en Hola **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c642b-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="c642b-181">d.</span><span class="sxs-lookup"><span data-stu-id="c642b-181">d.</span></span> <span data-ttu-id="c642b-182">Seleccione hello **es proveedor predeterminado** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="c642b-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="c642b-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c642b-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c642b-184">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c642b-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c642b-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c642b-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c642b-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c642b-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c642b-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c642b-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c642b-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c642b-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c642b-190">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c642b-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c642b-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c642b-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c642b-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c642b-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c642b-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c642b-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c642b-198">a.</span><span class="sxs-lookup"><span data-stu-id="c642b-198">a.</span></span> <span data-ttu-id="c642b-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c642b-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c642b-200">b.</span><span class="sxs-lookup"><span data-stu-id="c642b-200">b.</span></span> <span data-ttu-id="c642b-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c642b-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c642b-202">c.</span><span class="sxs-lookup"><span data-stu-id="c642b-202">c.</span></span> <span data-ttu-id="c642b-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c642b-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c642b-204">d.</span><span class="sxs-lookup"><span data-stu-id="c642b-204">d.</span></span> <span data-ttu-id="c642b-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c642b-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="c642b-206">Creación de un usuario de prueba de UNIFI</span><span class="sxs-lookup"><span data-stu-id="c642b-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="c642b-207">En esta sección, creará un usuario llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c642b-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="c642b-208">**UNIFI** admite el aprovisionamiento automático de usuarios, por lo que se requiere ningún paso manual.</span><span class="sxs-lookup"><span data-stu-id="c642b-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="c642b-209">Los usuarios se crean automáticamente tras la autenticación correcta de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c642b-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c642b-210">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c642b-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c642b-211">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooUNIFI.</span><span class="sxs-lookup"><span data-stu-id="c642b-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c642b-213">**tooassign Britta Simon tooUNIFI, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c642b-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="c642b-214">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c642b-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c642b-216">En la lista de aplicaciones de hello, seleccione **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="c642b-216">In hello applications list, select **UNIFI**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="c642b-218">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c642b-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c642b-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c642b-220">Click **Add** button.</span></span> <span data-ttu-id="c642b-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c642b-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c642b-223">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c642b-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c642b-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c642b-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c642b-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c642b-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c642b-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c642b-226">Testing single sign-on</span></span>

<span data-ttu-id="c642b-227">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c642b-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c642b-228">Al hacer clic en hello UNIFI el icono Panel de acceso de hello, deberá obtener la aplicación de UNIFI tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="c642b-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="c642b-229">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c642b-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c642b-230">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c642b-230">Additional resources</span></span>

* [<span data-ttu-id="c642b-231">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c642b-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c642b-232">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c642b-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

