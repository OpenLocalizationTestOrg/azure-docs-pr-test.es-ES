---
title: "Tutorial: Integración de Azure Active Directory con BenSelect | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="954cb-103">Tutorial: Integración de Azure Active Directory con BenSelect</span><span class="sxs-lookup"><span data-stu-id="954cb-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="954cb-104">En este tutorial, aprenderá cómo toointegrate BenSelect con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="954cb-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="954cb-105">Integración BenSelect con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="954cb-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="954cb-106">Puede controlar en Azure AD que tenga acceso tooBenSelect</span><span class="sxs-lookup"><span data-stu-id="954cb-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="954cb-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBenSelect (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="954cb-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="954cb-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="954cb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="954cb-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="954cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="954cb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="954cb-110">Prerequisites</span></span>

<span data-ttu-id="954cb-111">integración de Azure AD con BenSelect tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="954cb-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="954cb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="954cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="954cb-113">Una suscripción habilitada para el inicio de sesión único en BenSelect</span><span class="sxs-lookup"><span data-stu-id="954cb-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="954cb-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="954cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="954cb-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="954cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="954cb-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="954cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="954cb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="954cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="954cb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="954cb-118">Scenario description</span></span>
<span data-ttu-id="954cb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="954cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="954cb-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="954cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="954cb-121">Agregar BenSelect desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="954cb-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="954cb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="954cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="954cb-123">Agregar BenSelect desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="954cb-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="954cb-124">integración de hello tooconfigure de BenSelect en Azure AD, deberá tooadd BenSelect de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="954cb-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="954cb-125">**tooadd BenSelect de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="954cb-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="954cb-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="954cb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="954cb-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="954cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="954cb-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="954cb-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="954cb-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="954cb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="954cb-133">En el cuadro de búsqueda de hello, escriba **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="954cb-133">In hello search box, type **BenSelect**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="954cb-135">En el panel de resultados de hello, seleccione **BenSelect**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="954cb-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="954cb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="954cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="954cb-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BenSelect con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="954cb-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="954cb-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en BenSelect es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="954cb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="954cb-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en BenSelect debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="954cb-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="954cb-141">En BenSelect, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="954cb-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="954cb-142">tooconfigure y prueba de inicio de sesión único en Azure AD con BenSelect, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="954cb-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="954cb-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="954cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="954cb-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="954cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="954cb-145">**[Crear un usuario de prueba BenSelect](#creating-a-benselect-test-user)**  -toohave un equivalente de Britta Simon en BenSelect que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="954cb-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="954cb-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="954cb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="954cb-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="954cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="954cb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="954cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="954cb-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación BenSelect.</span><span class="sxs-lookup"><span data-stu-id="954cb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="954cb-150">**inicio de sesión único en Azure AD tooconfigure con BenSelect, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="954cb-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="954cb-151">En el portal de Azure, en Hola Hola **BenSelect** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="954cb-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="954cb-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="954cb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="954cb-155">En hello **BenSelect dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="954cb-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="954cb-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="954cb-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="954cb-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="954cb-158">This value is not real.</span></span> <span data-ttu-id="954cb-159">Actualizar este valor con la dirección URL de respuesta real Hola.</span><span class="sxs-lookup"><span data-stu-id="954cb-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="954cb-160">Póngase en contacto con [equipo de soporte técnico de BenSelect](mailto:support@selerix.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="954cb-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="954cb-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="954cb-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="954cb-163">Aplicación de BenSelect espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="954cb-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="954cb-164">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="954cb-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="954cb-165">Puede administrar valores de hello de estos atributos de hello **atributos de usuario** sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="954cb-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="954cb-166">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="954cb-166">hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="954cb-168">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="954cb-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="954cb-169">a.</span><span class="sxs-lookup"><span data-stu-id="954cb-169">a.</span></span> <span data-ttu-id="954cb-170">Hola **identificador de usuario** lista desplegable, seleccione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="954cb-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="954cb-171">b.</span><span class="sxs-lookup"><span data-stu-id="954cb-171">b.</span></span> <span data-ttu-id="954cb-172">Hola **correo** lista desplegable, seleccione **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="954cb-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="954cb-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="954cb-173">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="954cb-175">En hello **BenSelect configuración** sección, haga clic en **configurar BenSelect** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="954cb-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="954cb-176">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="954cb-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="954cb-178">inicio de sesión único en tooconfigure en **BenSelect** lado, necesita hello toosend descargado **Certificate(Raw)** y **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio**demasiado[equipo de soporte técnico de BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="954cb-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="954cb-179">Necesita toomention que esta integración requiere el algoritmo de hello SHA256 (no se admite SHA1) tooset Hola SSO en el servidor adecuado de hello como app2101 etcetera.</span><span class="sxs-lookup"><span data-stu-id="954cb-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="954cb-180">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="954cb-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="954cb-181">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="954cb-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="954cb-182">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="954cb-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="954cb-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="954cb-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="954cb-184">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="954cb-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="954cb-186">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="954cb-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="954cb-187">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="954cb-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="954cb-189">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="954cb-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="954cb-191">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="954cb-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="954cb-193">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="954cb-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="954cb-195">a.</span><span class="sxs-lookup"><span data-stu-id="954cb-195">a.</span></span> <span data-ttu-id="954cb-196">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="954cb-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="954cb-197">b.</span><span class="sxs-lookup"><span data-stu-id="954cb-197">b.</span></span> <span data-ttu-id="954cb-198">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="954cb-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="954cb-199">c.</span><span class="sxs-lookup"><span data-stu-id="954cb-199">c.</span></span> <span data-ttu-id="954cb-200">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="954cb-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="954cb-201">d.</span><span class="sxs-lookup"><span data-stu-id="954cb-201">d.</span></span> <span data-ttu-id="954cb-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="954cb-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="954cb-203">Creación de un usuario de prueba de BenSelect</span><span class="sxs-lookup"><span data-stu-id="954cb-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="954cb-204">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en BenSelect toocreate.</span><span class="sxs-lookup"><span data-stu-id="954cb-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="954cb-205">Trabajar con [equipo de soporte técnico de BenSelect](mailto:support@selerix.com) a los usuarios de tooadd Hola Hola BenSelect cuenta.</span><span class="sxs-lookup"><span data-stu-id="954cb-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="954cb-206">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="954cb-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="954cb-207">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBenSelect.</span><span class="sxs-lookup"><span data-stu-id="954cb-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="954cb-209">**tooassign Britta Simon tooBenSelect, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="954cb-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="954cb-210">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="954cb-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="954cb-212">En la lista de aplicaciones de hello, seleccione **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="954cb-212">In hello applications list, select **BenSelect**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="954cb-214">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="954cb-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="954cb-216">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="954cb-216">Click **Add** button.</span></span> <span data-ttu-id="954cb-217">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="954cb-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="954cb-219">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="954cb-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="954cb-220">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="954cb-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="954cb-221">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="954cb-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="954cb-222">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="954cb-222">Testing single sign-on</span></span>

<span data-ttu-id="954cb-223">En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="954cb-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="954cb-224">Al hacer clic en icono de BenSelect Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour BenSelect aplicación.</span><span class="sxs-lookup"><span data-stu-id="954cb-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="954cb-225">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="954cb-225">Additional resources</span></span>

* [<span data-ttu-id="954cb-226">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="954cb-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="954cb-227">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="954cb-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

