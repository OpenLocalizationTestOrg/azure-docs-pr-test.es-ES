---
title: "Tutorial: Integración de Azure Active Directory con Bambu by Sprout Social | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Bambu por brotes sociales."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="17b44-103">Tutorial: Integración de Azure Active Directory con Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="17b44-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="17b44-104">En este tutorial, aprenderá cómo toointegrate Bambu por brotes sociales con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17b44-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17b44-105">Integración Bambu por brotes sociales con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="17b44-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17b44-106">Puede controlar en Azure AD que tenga acceso tooBambu por brotes sociales</span><span class="sxs-lookup"><span data-stu-id="17b44-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="17b44-107">Puede habilitar la get ha iniciado sesión tooBambu de usuarios tooautomatically por brotes sociales (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b44-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17b44-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="17b44-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17b44-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17b44-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="17b44-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="17b44-110">Prerequisites</span></span>

<span data-ttu-id="17b44-111">tooconfigure integración de Azure AD con Bambu por brotes sociales, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="17b44-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="17b44-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b44-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17b44-113">Una suscripción habilitada para el inicio de sesión único en Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="17b44-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17b44-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="17b44-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17b44-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="17b44-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17b44-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="17b44-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="17b44-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17b44-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17b44-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="17b44-118">Scenario description</span></span>
<span data-ttu-id="17b44-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="17b44-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17b44-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="17b44-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17b44-121">Agregar Bambu por brotes sociales de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="17b44-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="17b44-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b44-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="17b44-123">Agregar Bambu por brotes sociales de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="17b44-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="17b44-124">integración de hello tooconfigure de Bambu por brotes sociales en Azure AD, deberá tooadd Bambu por brotes sociales de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="17b44-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17b44-125">**tooadd Bambu por brotes sociales de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17b44-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17b44-126">Hola  **[Portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="17b44-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17b44-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="17b44-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17b44-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17b44-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="17b44-131">Haga clic en **nueva aplicación** botón en la parte superior de Hola de nueva aplicación de hello diálogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="17b44-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="17b44-133">En el cuadro de búsqueda de hello, escriba **Bambu por brotes sociales**.</span><span class="sxs-lookup"><span data-stu-id="17b44-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="17b44-135">En el panel de resultados de hello, seleccione **Bambu por brotes sociales**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="17b44-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17b44-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b44-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17b44-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Bambu by Sprout Social con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="17b44-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17b44-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Bambu por brotes sociales es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17b44-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="17b44-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Bambu por brotes sociales debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="17b44-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="17b44-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Bambu por brotes sociales.</span><span class="sxs-lookup"><span data-stu-id="17b44-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="17b44-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Bambu por brotes sociales, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="17b44-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17b44-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="17b44-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17b44-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17b44-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17b44-145">**[Crear un Bambu por usuario de prueba de los brotes sociales](#creating-a-bambu-by-sprout-social-test-user)**  -toohave un equivalente de Britta Simon en Bambu por brotes Social que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="17b44-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="17b44-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="17b44-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17b44-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="17b44-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17b44-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b44-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17b44-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su Bambu aplicando los brotes sociales.</span><span class="sxs-lookup"><span data-stu-id="17b44-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="17b44-150">**tooconfigure inicio de sesión único en Azure AD con Bambu por brotes sociales, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17b44-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="17b44-151">En el portal de Azure, en Hola Hola **Bambu por brotes sociales** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="17b44-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="17b44-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="17b44-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="17b44-155">En hello **Bambu brotes sociales dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="17b44-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="17b44-157">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="17b44-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="17b44-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="17b44-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="17b44-161">En hello **Bambu brotes sociales configuración** sección, haga clic en **Bambu configurar por brotes sociales** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="17b44-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="17b44-162">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="17b44-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="17b44-164">tooconfigure inicio de sesión único en **Bambu por brotes sociales** lado, necesita hello toosend descargado **Metadata XML** y **SAML Single Sign-On dirección URL del servicio** demasiado[Bambu por compatibilidad con los brotes sociales](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="17b44-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="17b44-165">Configurará esto Hola de toohave orden configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="17b44-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="17b44-166">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="17b44-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17b44-167">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="17b44-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17b44-168">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17b44-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17b44-169">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b44-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="17b44-170">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="17b44-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="17b44-172">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17b44-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17b44-173">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="17b44-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17b44-175">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="17b44-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17b44-177">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17b44-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17b44-179">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="17b44-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17b44-181">a.</span><span class="sxs-lookup"><span data-stu-id="17b44-181">a.</span></span> <span data-ttu-id="17b44-182">Hola **nombre** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="17b44-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="17b44-183">b.</span><span class="sxs-lookup"><span data-stu-id="17b44-183">b.</span></span> <span data-ttu-id="17b44-184">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17b44-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="17b44-185">c.</span><span class="sxs-lookup"><span data-stu-id="17b44-185">c.</span></span> <span data-ttu-id="17b44-186">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="17b44-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17b44-187">d.</span><span class="sxs-lookup"><span data-stu-id="17b44-187">d.</span></span> <span data-ttu-id="17b44-188">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="17b44-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="17b44-189">Creación de un usuario de prueba de Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="17b44-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="17b44-190">Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de que los usuarios de autenticación se creará en la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="17b44-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17b44-191">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b44-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17b44-192">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooBambu acceso por brotes sociales.</span><span class="sxs-lookup"><span data-stu-id="17b44-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="17b44-194">**tooassign Britta Simon tooBambu por brotes sociales, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17b44-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="17b44-195">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17b44-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="17b44-197">En la lista de aplicaciones de hello, seleccione **Bambu por brotes sociales**.</span><span class="sxs-lookup"><span data-stu-id="17b44-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="17b44-199">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17b44-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="17b44-201">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="17b44-201">Click **Add** button.</span></span> <span data-ttu-id="17b44-202">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17b44-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="17b44-204">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="17b44-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17b44-205">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17b44-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17b44-206">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17b44-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17b44-207">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="17b44-207">Testing single sign-on</span></span>

<span data-ttu-id="17b44-208">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="17b44-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="17b44-209">Al hacer clic en hello Bambu por brotes sociales mosaico Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Bambu aplicación brotes sociales.</span><span class="sxs-lookup"><span data-stu-id="17b44-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="17b44-210">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="17b44-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="17b44-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="17b44-211">Additional resources</span></span>

* [<span data-ttu-id="17b44-212">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17b44-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17b44-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17b44-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

