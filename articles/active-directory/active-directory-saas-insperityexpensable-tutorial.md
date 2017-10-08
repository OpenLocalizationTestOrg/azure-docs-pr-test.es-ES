---
title: "Tutorial: Integración de Azure Active Directory con Insperity ExpensAble | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 204d5435c6ba1f23bb98701381e165a9a66add62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="fb3c2-103">Tutorial: integración de Azure Active Directory con Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="fb3c2-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="fb3c2-104">En este tutorial, aprenderá cómo toointegrate Insperity ExpensAble con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb3c2-104">In this tutorial, you learn how toointegrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb3c2-105">Integración Insperity ExpensAble con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fb3c2-105">Integrating Insperity ExpensAble with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb3c2-106">Puede controlar en Azure AD que tenga acceso tooInsperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="fb3c2-106">You can control in Azure AD who has access tooInsperity ExpensAble</span></span>
- <span data-ttu-id="fb3c2-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooInsperity ExpensAble (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb3c2-107">You can enable your users tooautomatically get signed-on tooInsperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb3c2-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fb3c2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fb3c2-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb3c2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb3c2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb3c2-110">Prerequisites</span></span>

<span data-ttu-id="fb3c2-111">integración de Azure AD con Insperity ExpensAble tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fb3c2-111">tooconfigure Azure AD integration with Insperity ExpensAble, you need hello following items:</span></span>

- <span data-ttu-id="fb3c2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb3c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb3c2-113">Una suscripción habilitada para el inicio de sesión único en Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="fb3c2-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb3c2-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb3c2-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fb3c2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb3c2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb3c2-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb3c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb3c2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fb3c2-118">Scenario description</span></span>
<span data-ttu-id="fb3c2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb3c2-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="fb3c2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb3c2-121">Agregar Insperity ExpensAble desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fb3c2-121">Adding Insperity ExpensAble from hello gallery</span></span>
2. <span data-ttu-id="fb3c2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb3c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-hello-gallery"></a><span data-ttu-id="fb3c2-123">Agregar Insperity ExpensAble desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fb3c2-123">Adding Insperity ExpensAble from hello gallery</span></span>
<span data-ttu-id="fb3c2-124">integración de hello tooconfigure de Insperity ExpensAble en Azure AD, deberá tooadd Insperity ExpensAble de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-124">tooconfigure hello integration of Insperity ExpensAble into Azure AD, you need tooadd Insperity ExpensAble from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb3c2-125">**tooadd Insperity ExpensAble de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb3c2-125">**tooadd Insperity ExpensAble from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb3c2-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb3c2-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb3c2-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fb3c2-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fb3c2-133">En el cuadro de búsqueda de hello, escriba **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-133">In hello search box, type **Insperity ExpensAble**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="fb3c2-135">En el panel de resultados de hello, seleccione **Insperity ExpensAble**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-135">In hello results panel, select **Insperity ExpensAble**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb3c2-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb3c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb3c2-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Insperity ExpensAble con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb3c2-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb3c2-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Insperity ExpensAble es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Insperity ExpensAble is tooa user in Azure AD.</span></span> <span data-ttu-id="fb3c2-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Insperity ExpensAble debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-140">In other words, a link relationship between an Azure AD user and hello related user in Insperity ExpensAble needs toobe established.</span></span>

<span data-ttu-id="fb3c2-141">En Insperity ExpensAble, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-141">In Insperity ExpensAble, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fb3c2-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Insperity ExpensAble, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fb3c2-142">tooconfigure and test Azure AD single sign-on with Insperity ExpensAble, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb3c2-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb3c2-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb3c2-145">**[Creación de un usuario de prueba Insperity ExpensAble](#creating-an-insperity-expensable-test-user)**  -toohave un equivalente de Britta Simon en Insperity ExpensAble que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - toohave a counterpart of Britta Simon in Insperity ExpensAble that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb3c2-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb3c2-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb3c2-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb3c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb3c2-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="fb3c2-150">**inicio de sesión único en Azure AD tooconfigure con Insperity ExpensAble, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb3c2-150">**tooconfigure Azure AD single sign-on with Insperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb3c2-151">En el portal de Azure, en Hola Hola **Insperity ExpensAble** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-151">In hello Azure portal, on hello **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fb3c2-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="fb3c2-155">En hello **Insperity ExpensAble dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fb3c2-155">On hello **Insperity ExpensAble Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="fb3c2-157">a.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-157">a.</span></span> <span data-ttu-id="fb3c2-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="fb3c2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fb3c2-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-159">This value is not real.</span></span> <span data-ttu-id="fb3c2-160">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="fb3c2-161">Póngase en contacto con [equipo de soporte técnico de cliente ExpensAble Insperity](http://expensable.com/support/support-overview) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) tooget this value.</span></span> 
 
4. <span data-ttu-id="fb3c2-162">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="fb3c2-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fb3c2-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb3c2-166">En hello **Insperity ExpensAble configuración** sección, haga clic en **configurar Insperity ExpensAble** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-166">On hello **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fb3c2-167">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="fb3c2-167">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="fb3c2-169">inicio de sesión único en tooconfigure en **Insperity ExpensAble** lado, necesita hello toosend descargado **Metadata XML**, **SAML Single Sign-On dirección URL del servicio** y **Id. de entidad SAML** demasiado[Insperity ExpensAble equipo de soporte técnico](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="fb3c2-169">tooconfigure single sign-on on **Insperity ExpensAble** side, you need toosend hello downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="fb3c2-170">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fb3c2-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="fb3c2-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb3c2-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb3c2-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb3c2-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb3c2-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb3c2-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb3c2-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fb3c2-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb3c2-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb3c2-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb3c2-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb3c2-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb3c2-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="fb3c2-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb3c2-186">a.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-186">a.</span></span> <span data-ttu-id="fb3c2-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb3c2-188">b.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-188">b.</span></span> <span data-ttu-id="fb3c2-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb3c2-190">c.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-190">c.</span></span> <span data-ttu-id="fb3c2-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fb3c2-192">d.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-192">d.</span></span> <span data-ttu-id="fb3c2-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="fb3c2-194">Creación de un usuario de prueba de Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="fb3c2-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="fb3c2-195">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Insperity ExpensAble toocreate.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-195">hello objective of this section is toocreate a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="fb3c2-196">Trabaje con [Insperity ExpensAble equipo de soporte técnico](http://expensable.com/support/support-overview) a los usuarios de tooadd Hola Hola Insperity ExpensAble cuenta.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) tooadd hello users in hello Insperity ExpensAble account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fb3c2-197">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb3c2-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fb3c2-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooInsperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsperity ExpensAble.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fb3c2-200">**tooassign tooInsperity Britta Simon ExpensAble, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb3c2-200">**tooassign Britta Simon tooInsperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb3c2-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fb3c2-203">En la lista de aplicaciones de hello, seleccione **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-203">In hello applications list, select **Insperity ExpensAble**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="fb3c2-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fb3c2-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-207">Click **Add** button.</span></span> <span data-ttu-id="fb3c2-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fb3c2-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb3c2-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb3c2-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb3c2-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fb3c2-213">Testing single sign-on</span></span>

<span data-ttu-id="fb3c2-214">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fb3c2-215">Al hacer clic en icono Insperity ExpensAble Hola Hola Panel de acceso, deberá obtener la aplicación Insperity ExpensAble tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="fb3c2-215">When you click hello Insperity ExpensAble tile in hello Access Panel, you should get automatically signed-on tooyour Insperity ExpensAble application.</span></span>
<span data-ttu-id="fb3c2-216">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fb3c2-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb3c2-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fb3c2-217">Additional resources</span></span>

* [<span data-ttu-id="fb3c2-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb3c2-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb3c2-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb3c2-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

