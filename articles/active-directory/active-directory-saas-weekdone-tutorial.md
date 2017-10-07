---
title: "Tutorial: Integración de Azure Active Directory con Weekdone | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="a73db-103">Tutorial: Integración de Azure Active Directory con Weekdone</span><span class="sxs-lookup"><span data-stu-id="a73db-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="a73db-104">En este tutorial, aprenderá cómo toointegrate Weekdone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a73db-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a73db-105">Integración Weekdone con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a73db-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a73db-106">Puede controlar en Azure AD que tenga acceso tooWeekdone</span><span class="sxs-lookup"><span data-stu-id="a73db-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="a73db-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWeekdone (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a73db-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a73db-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a73db-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a73db-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a73db-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a73db-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a73db-110">Prerequisites</span></span>

<span data-ttu-id="a73db-111">integración de Azure AD con Weekdone tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a73db-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="a73db-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a73db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a73db-113">Una suscripción habilitada para inicio de sesión único en Weekdone</span><span class="sxs-lookup"><span data-stu-id="a73db-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a73db-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a73db-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a73db-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a73db-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a73db-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a73db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a73db-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a73db-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a73db-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a73db-118">Scenario description</span></span>
<span data-ttu-id="a73db-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a73db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a73db-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="a73db-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a73db-121">Agregar Weekdone desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a73db-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="a73db-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a73db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="a73db-123">Agregar Weekdone desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a73db-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="a73db-124">integración de hello tooconfigure de Weekdone en Azure AD, deberá tooadd Weekdone de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a73db-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a73db-125">**tooadd Weekdone de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a73db-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73db-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a73db-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a73db-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a73db-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a73db-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a73db-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a73db-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a73db-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a73db-133">En el cuadro de búsqueda de hello, escriba **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="a73db-133">In hello search box, type **Weekdone**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="a73db-135">En el panel de resultados de hello, seleccione **Weekdone**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a73db-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a73db-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a73db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a73db-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Weekdone con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a73db-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a73db-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Weekdone es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a73db-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="a73db-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Weekdone debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="a73db-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="a73db-141">En Weekdone, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a73db-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a73db-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Weekdone, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a73db-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a73db-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="a73db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a73db-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a73db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a73db-145">**[Crear un usuario de prueba Weekdone](#creating-a-weekdone-test-user) ** -toohave un equivalente de Britta Simon en Weekdone que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="a73db-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a73db-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a73db-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a73db-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a73db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a73db-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a73db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a73db-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Weekdone.</span><span class="sxs-lookup"><span data-stu-id="a73db-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="a73db-150">**inicio de sesión único en Azure AD tooconfigure con Weekdone, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a73db-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73db-151">En el portal de Azure, en Hola Hola **Weekdone** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a73db-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a73db-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a73db-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="a73db-155">En hello **Weekdone dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="a73db-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="a73db-157">a.</span><span class="sxs-lookup"><span data-stu-id="a73db-157">a.</span></span> <span data-ttu-id="a73db-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="a73db-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="a73db-159">b.</span><span class="sxs-lookup"><span data-stu-id="a73db-159">b.</span></span> <span data-ttu-id="a73db-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="a73db-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="a73db-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="a73db-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a73db-162">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="a73db-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="a73db-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="a73db-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a73db-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="a73db-165">These values are not real.</span></span> <span data-ttu-id="a73db-166">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a73db-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a73db-167">Póngase en contacto con [equipo de soporte técnico de cliente de Weekdone](mailto:hello@weekdone.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="a73db-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="a73db-168">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a73db-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="a73db-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a73db-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a73db-172">En hello **Weekdone configuración** sección, haga clic en **configurar Weekdone** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="a73db-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a73db-173">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="a73db-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="a73db-175">tooconfigure inicio de sesión único en **Weekdone** lado, necesita hello toosend descargado **Metadata XML, dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado[Weekdone compatibilidad equipo](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="a73db-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="a73db-176">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="a73db-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a73db-177">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="a73db-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a73db-178">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a73db-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a73db-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a73db-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="a73db-180">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="a73db-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a73db-182">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a73db-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73db-183">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a73db-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a73db-185">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a73db-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a73db-187">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a73db-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a73db-189">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="a73db-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a73db-191">a.</span><span class="sxs-lookup"><span data-stu-id="a73db-191">a.</span></span> <span data-ttu-id="a73db-192">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a73db-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a73db-193">b.</span><span class="sxs-lookup"><span data-stu-id="a73db-193">b.</span></span> <span data-ttu-id="a73db-194">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a73db-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a73db-195">c.</span><span class="sxs-lookup"><span data-stu-id="a73db-195">c.</span></span> <span data-ttu-id="a73db-196">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a73db-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a73db-197">d.</span><span class="sxs-lookup"><span data-stu-id="a73db-197">d.</span></span> <span data-ttu-id="a73db-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a73db-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="a73db-199">Creación de un usuario de prueba de Weekdone</span><span class="sxs-lookup"><span data-stu-id="a73db-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="a73db-200">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Weekdone toocreate.</span><span class="sxs-lookup"><span data-stu-id="a73db-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="a73db-201">Weekdone admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a73db-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a73db-202">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="a73db-202">There is no action item for you in this section.</span></span> <span data-ttu-id="a73db-203">Se crea un nuevo usuario durante un tooaccess intento Weekdone si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="a73db-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a73db-204">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de Weekdone cliente](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="a73db-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a73db-205">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a73db-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a73db-206">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWeekdone.</span><span class="sxs-lookup"><span data-stu-id="a73db-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a73db-208">**tooassign Britta Simon tooWeekdone, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a73db-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73db-209">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a73db-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a73db-211">En la lista de aplicaciones de hello, seleccione **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="a73db-211">In hello applications list, select **Weekdone**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="a73db-213">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a73db-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a73db-215">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a73db-215">Click **Add** button.</span></span> <span data-ttu-id="a73db-216">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a73db-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a73db-218">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="a73db-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a73db-219">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a73db-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a73db-220">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a73db-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a73db-221">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a73db-221">Testing single sign-on</span></span>

<span data-ttu-id="a73db-222">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a73db-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a73db-223">Al hacer clic en icono de Weekdone Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Weekdone aplicación.</span><span class="sxs-lookup"><span data-stu-id="a73db-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a73db-224">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a73db-224">Additional resources</span></span>

* [<span data-ttu-id="a73db-225">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a73db-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a73db-226">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a73db-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

