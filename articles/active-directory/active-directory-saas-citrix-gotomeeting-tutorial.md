---
title: "Tutorial: Integración de Azure Active Directory con Citrix GoToMeeting | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="8dc54-103">Tutorial: Integración de Azure Active Directory con Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="8dc54-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="8dc54-104">En este tutorial, aprenderá cómo toointegrate Citrix GoToMeeting con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8dc54-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8dc54-105">Integración de Citrix GoToMeeting con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8dc54-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8dc54-106">Puede controlar en Azure AD que tenga acceso tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="8dc54-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="8dc54-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCitrix GoToMeeting (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc54-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8dc54-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8dc54-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8dc54-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8dc54-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dc54-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8dc54-110">Prerequisites</span></span>

<span data-ttu-id="8dc54-111">tooconfigure integración de Azure AD con Citrix GoToMeeting, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8dc54-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="8dc54-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc54-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8dc54-113">Una suscripción habilitada para el inicio de sesión único en Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="8dc54-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8dc54-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8dc54-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8dc54-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8dc54-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8dc54-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8dc54-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8dc54-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8dc54-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8dc54-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8dc54-118">Scenario description</span></span>
<span data-ttu-id="8dc54-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8dc54-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8dc54-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8dc54-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8dc54-121">Adición de Citrix GoToMeeting desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="8dc54-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="8dc54-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc54-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="8dc54-123">Adición de Citrix GoToMeeting desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="8dc54-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="8dc54-124">integración de hello tooconfigure de Citrix GoToMeeting en Azure AD, deberá tooadd Citrix GoToMeeting de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8dc54-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8dc54-125">**tooadd Citrix GoToMeeting de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8dc54-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dc54-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8dc54-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8dc54-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8dc54-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8dc54-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc54-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8dc54-133">En el cuadro de búsqueda de hello, escriba **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="8dc54-135">En el panel de resultados de hello, seleccione **Citrix GoToMeeting**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8dc54-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8dc54-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc54-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8dc54-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Citrix GoToMeeting con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8dc54-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8dc54-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Citrix GoToMeeting es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dc54-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="8dc54-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Citrix GoToMeeting debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8dc54-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="8dc54-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="8dc54-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="8dc54-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Citrix GoToMeeting, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8dc54-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8dc54-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8dc54-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8dc54-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8dc54-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8dc54-145">**[Crear un usuario de prueba de Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave un equivalente de Britta Simon en Citrix GoToMeeting que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8dc54-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8dc54-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8dc54-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8dc54-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8dc54-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8dc54-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc54-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8dc54-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="8dc54-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="8dc54-150">**inicio de sesión único en tooconfigure Azure AD con Citrix GoToMeeting, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8dc54-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dc54-151">En el portal de Azure, en Hola Hola **Citrix GoToMeeting** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8dc54-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8dc54-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="8dc54-155">En hello **Citrix GoToMeeting dominio y las direcciones URL** no sección, necesidad de tooperform todos los pasos.</span><span class="sxs-lookup"><span data-stu-id="8dc54-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="8dc54-157">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8dc54-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="8dc54-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8dc54-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="8dc54-161">En la sección de configuración de SAML de Citrix GoToMeeting hello, haga clic en configurar Citrix GoToMeeting SAML tooopen configurar inicio de sesión en la ventana.</span><span class="sxs-lookup"><span data-stu-id="8dc54-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="8dc54-162">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8dc54-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="8dc54-163">En otra ventana del explorador, inicie sesión en tooyour [Center de organización de Citrix](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="8dc54-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="8dc54-164">Haga clic en hello **proveedor de identidades** pestaña y, a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8dc54-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="8dc54-165">![Configuración de SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="8dc54-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="8dc54-166">a.</span><span class="sxs-lookup"><span data-stu-id="8dc54-166">a.</span></span> <span data-ttu-id="8dc54-167">Seleccione **Manual**</span><span class="sxs-lookup"><span data-stu-id="8dc54-167">Select **Manual**</span></span>

    <span data-ttu-id="8dc54-168">b.</span><span class="sxs-lookup"><span data-stu-id="8dc54-168">b.</span></span> <span data-ttu-id="8dc54-169">En el portal de Azure, en Hola Hola **configurar inicio de sesión único en Citrix GoToMeeting** página de diálogo, Hola copia **SAML Single Sign-On dirección URL del servicio** valor y, a continuación, péguelo en hello **página de inicio de sesión Dirección URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8dc54-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="8dc54-170">c.</span><span class="sxs-lookup"><span data-stu-id="8dc54-170">c.</span></span> <span data-ttu-id="8dc54-171">En el portal de Azure, en Hola Hola **configurar inicio de sesión único en Citrix GoToMeeting** página de diálogo, Hola copia **dirección URL de cierre de sesión** valor y, a continuación, péguelo en hello **URL de la página de cierre de sesión**cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8dc54-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="8dc54-172">d.</span><span class="sxs-lookup"><span data-stu-id="8dc54-172">d.</span></span> <span data-ttu-id="8dc54-173">En el portal de Azure, en Hola Hola **configurar inicio de sesión único en Citrix GoToMeeting** página de diálogo, Hola copia **Id. de entidad SAML** valor y, a continuación, péguelo en hello **Id. de entidad de proveedor de identidad**  cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8dc54-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="8dc54-174">e.</span><span class="sxs-lookup"><span data-stu-id="8dc54-174">e.</span></span> <span data-ttu-id="8dc54-175">tooupload el certificado descargado, haga clic en **cargar certificado**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="8dc54-176">f.</span><span class="sxs-lookup"><span data-stu-id="8dc54-176">f.</span></span> <span data-ttu-id="8dc54-177">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8dc54-178">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8dc54-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8dc54-179">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc54-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8dc54-180">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8dc54-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8dc54-181">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc54-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="8dc54-182">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8dc54-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8dc54-184">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8dc54-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dc54-185">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8dc54-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8dc54-187">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8dc54-189">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc54-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8dc54-191">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8dc54-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8dc54-193">a.</span><span class="sxs-lookup"><span data-stu-id="8dc54-193">a.</span></span> <span data-ttu-id="8dc54-194">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8dc54-195">b.</span><span class="sxs-lookup"><span data-stu-id="8dc54-195">b.</span></span> <span data-ttu-id="8dc54-196">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8dc54-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8dc54-197">c.</span><span class="sxs-lookup"><span data-stu-id="8dc54-197">c.</span></span> <span data-ttu-id="8dc54-198">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8dc54-199">d.</span><span class="sxs-lookup"><span data-stu-id="8dc54-199">d.</span></span> <span data-ttu-id="8dc54-200">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="8dc54-201">Creación de un usuario de prueba de Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="8dc54-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="8dc54-202">En esta sección, creará un usuario llamado a Britta Simon en Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="8dc54-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="8dc54-203">Citrix GoToMeeting admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8dc54-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8dc54-204">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8dc54-204">There is no action item for you in this section.</span></span> <span data-ttu-id="8dc54-205">Si un usuario ya no existe en Citrix GoToMeeting, se crea uno nuevo cuando intente tooaccess Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="8dc54-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="8dc54-206">Si necesita toocreate manualmente, póngase en contacto con en un usuario [equipo de soporte técnico de Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="8dc54-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8dc54-207">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc54-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8dc54-208">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="8dc54-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8dc54-210">**tooassign Britta Simon tooCitrix GoToMeeting, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8dc54-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dc54-211">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8dc54-213">En la lista de aplicaciones de hello, seleccione **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="8dc54-215">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8dc54-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-217">Click **Add** button.</span></span> <span data-ttu-id="8dc54-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8dc54-220">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8dc54-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8dc54-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8dc54-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8dc54-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8dc54-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8dc54-223">Testing single sign-on</span></span>

<span data-ttu-id="8dc54-224">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8dc54-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8dc54-225">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8dc54-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="8dc54-226">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dc54-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8dc54-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8dc54-227">Additional resources</span></span>

* [<span data-ttu-id="8dc54-228">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dc54-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8dc54-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8dc54-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8dc54-230">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="8dc54-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

