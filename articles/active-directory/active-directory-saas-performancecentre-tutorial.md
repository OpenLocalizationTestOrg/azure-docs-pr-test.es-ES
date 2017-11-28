---
title: "Tutorial: Integración de Azure Active Directory con PerformanceCentre | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="67928-103">Tutorial: Integración de Azure Active Directory con PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="67928-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="67928-104">En este tutorial, aprenderá cómo toointegrate PerformanceCentre con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67928-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67928-105">Integración PerformanceCentre con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="67928-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="67928-106">Puede controlar en Azure AD que tenga acceso tooPerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="67928-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="67928-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPerformanceCentre (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="67928-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67928-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="67928-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="67928-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67928-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67928-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="67928-110">Prerequisites</span></span>

<span data-ttu-id="67928-111">integración de Azure AD con PerformanceCentre tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="67928-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="67928-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="67928-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67928-113">Una suscripción habilitada para el inicio de sesión único en PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="67928-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67928-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="67928-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67928-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="67928-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67928-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="67928-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67928-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67928-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67928-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="67928-118">Scenario description</span></span>
<span data-ttu-id="67928-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="67928-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67928-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="67928-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67928-121">Agregar PerformanceCentre desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="67928-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="67928-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="67928-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="67928-123">Agregar PerformanceCentre desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="67928-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="67928-124">integración de hello tooconfigure de PerformanceCentre en Azure AD, deberá tooadd PerformanceCentre de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="67928-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="67928-125">**tooadd PerformanceCentre de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="67928-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="67928-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="67928-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67928-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="67928-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="67928-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="67928-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="67928-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="67928-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="67928-133">En el cuadro de búsqueda de hello, escriba **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="67928-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="67928-135">En el panel de resultados de hello, seleccione **PerformanceCentre**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="67928-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67928-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="67928-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67928-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con PerformanceCentre con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="67928-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="67928-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PerformanceCentre es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67928-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="67928-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PerformanceCentre debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="67928-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="67928-141">En PerformanceCentre, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="67928-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="67928-142">tooconfigure y prueba de inicio de sesión único en Azure AD con PerformanceCentre, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="67928-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="67928-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="67928-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="67928-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67928-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67928-145">**[Crear un usuario de prueba PerformanceCentre](#creating-a-performancecentre-test-user) ** -toohave un equivalente de Britta Simon en PerformanceCentre que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="67928-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="67928-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="67928-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67928-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="67928-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67928-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="67928-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67928-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="67928-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="67928-150">**inicio de sesión único en Azure AD tooconfigure con PerformanceCentre, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="67928-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="67928-151">En el portal de Azure, en Hola Hola **PerformanceCentre** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="67928-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="67928-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="67928-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="67928-155">En hello **PerformanceCentre dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="67928-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="67928-157">a.</span><span class="sxs-lookup"><span data-stu-id="67928-157">a.</span></span> <span data-ttu-id="67928-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="67928-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="67928-159">b.</span><span class="sxs-lookup"><span data-stu-id="67928-159">b.</span></span> <span data-ttu-id="67928-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="67928-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67928-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="67928-161">These values are not real.</span></span> <span data-ttu-id="67928-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="67928-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="67928-163">Póngase en contacto con [equipo de soporte técnico de cliente de PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="67928-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="67928-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="67928-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="67928-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="67928-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67928-168">En hello **PerformanceCentre configuración** sección, haga clic en **configurar PerformanceCentre** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="67928-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="67928-169">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="67928-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="67928-171">Inicio de sesión tooyour **PerformanceCentre** como administrador.</span><span class="sxs-lookup"><span data-stu-id="67928-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="67928-172">En la ficha de hello en el lado izquierdo de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="67928-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][10]

9. <span data-ttu-id="67928-174">En la ficha de hello en el lado izquierdo de hello, haga clic en **varios**y, a continuación, haga clic en **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="67928-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][11]

10. <span data-ttu-id="67928-176">En **Protocolo**, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="67928-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][12]

11. <span data-ttu-id="67928-178">Abra el archivo de metadatos descargado en el Bloc de notas, copiar el contenido de hello, péguela en hello **metadatos del proveedor de identidades** cuadro de texto y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="67928-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][13]

12. <span data-ttu-id="67928-180">Compruebe que los valores de hello para Hola **dirección URL de la Base de entidad** y **URL de Id. de entidad** son correctos.</span><span class="sxs-lookup"><span data-stu-id="67928-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Inicio de sesión único de Azure AD ][14]

> [!TIP]
> <span data-ttu-id="67928-182">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="67928-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="67928-183">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="67928-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="67928-184">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="67928-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67928-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="67928-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="67928-186">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="67928-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="67928-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="67928-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="67928-189">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="67928-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67928-191">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="67928-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67928-193">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="67928-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67928-195">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="67928-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67928-197">a.</span><span class="sxs-lookup"><span data-stu-id="67928-197">a.</span></span> <span data-ttu-id="67928-198">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67928-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67928-199">b.</span><span class="sxs-lookup"><span data-stu-id="67928-199">b.</span></span> <span data-ttu-id="67928-200">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="67928-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67928-201">c.</span><span class="sxs-lookup"><span data-stu-id="67928-201">c.</span></span> <span data-ttu-id="67928-202">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="67928-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="67928-203">d.</span><span class="sxs-lookup"><span data-stu-id="67928-203">d.</span></span> <span data-ttu-id="67928-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="67928-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="67928-205">Creación de un usuario de prueba de PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="67928-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="67928-206">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en PerformanceCentre toocreate.</span><span class="sxs-lookup"><span data-stu-id="67928-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="67928-207">**toocreate un usuario llamado Britta Simon en PerformanceCentre, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="67928-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="67928-208">Inicie sesión en tooyour PerformanceCentre sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="67928-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="67928-209">En el menú de Hola Hola izquierda, haga clic en **Interrelate**y, a continuación, haga clic en **crear participante**.</span><span class="sxs-lookup"><span data-stu-id="67928-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Crear usuario][400]

3. <span data-ttu-id="67928-211">En hello **se interrelacionan: crear participante** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="67928-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Crear usuario][401]
    
    <span data-ttu-id="67928-213">a.</span><span class="sxs-lookup"><span data-stu-id="67928-213">a.</span></span> <span data-ttu-id="67928-214">Hola de tipo los atributos requeridos para Britta Simon en cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="67928-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="67928-215">Nombre de usuario de Bárbara atributo de PerformanceCentre debe ser Hola igual Hola nombre de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67928-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="67928-216">b.</span><span class="sxs-lookup"><span data-stu-id="67928-216">b.</span></span> <span data-ttu-id="67928-217">Seleccione **Administrador de cliente** como **Elegir rol**.</span><span class="sxs-lookup"><span data-stu-id="67928-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="67928-218">c.</span><span class="sxs-lookup"><span data-stu-id="67928-218">c.</span></span> <span data-ttu-id="67928-219">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="67928-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="67928-220">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="67928-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="67928-221">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="67928-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="67928-223">**tooassign Britta Simon tooPerformanceCentre, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="67928-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="67928-224">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="67928-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="67928-226">En la lista de aplicaciones de hello, seleccione **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="67928-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="67928-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="67928-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="67928-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="67928-230">Click **Add** button.</span></span> <span data-ttu-id="67928-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="67928-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="67928-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="67928-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="67928-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="67928-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67928-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="67928-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67928-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="67928-236">Testing single sign-on</span></span>

<span data-ttu-id="67928-237">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="67928-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="67928-238">Al hacer clic en icono de PerformanceCentre Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour PerformanceCentre aplicación.</span><span class="sxs-lookup"><span data-stu-id="67928-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67928-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="67928-239">Additional resources</span></span>

* [<span data-ttu-id="67928-240">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67928-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67928-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="67928-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

