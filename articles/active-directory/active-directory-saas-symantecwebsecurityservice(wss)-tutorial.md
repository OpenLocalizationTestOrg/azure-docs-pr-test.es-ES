---
title: "Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el servicio de seguridad de Web (WSS) de Symantec."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="9d14c-103">Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="9d14c-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="9d14c-104">En este tutorial, aprenderá cómo toointegrate Symantec Web seguridad Service (WSS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d14c-104">In this tutorial, you learn how toointegrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d14c-105">Integración de servicios de seguridad Web de Symantec (WSS) con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9d14c-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9d14c-106">Puede controlar en Azure AD que tenga acceso tooSymantec Web seguridad Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="9d14c-106">You can control in Azure AD who has access tooSymantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="9d14c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSymantec Web seguridad Service (WSS) (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d14c-107">You can enable your users tooautomatically get signed-on tooSymantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d14c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9d14c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9d14c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d14c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d14c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d14c-110">Prerequisites</span></span>

<span data-ttu-id="9d14c-111">tooconfigure integración de Azure AD con el servicio de seguridad Web de Symantec (WSS), necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9d14c-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="9d14c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d14c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d14c-113">Una suscripción de Symantec Web Security Service (WSS) con inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="9d14c-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d14c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9d14c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d14c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9d14c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d14c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9d14c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d14c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d14c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d14c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9d14c-118">Scenario description</span></span>
<span data-ttu-id="9d14c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9d14c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d14c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9d14c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d14c-121">Agregar servicio de seguridad de Web de Symantec (WSS) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9d14c-121">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
2. <span data-ttu-id="9d14c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d14c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="9d14c-123">Agregar servicio de seguridad de Web de Symantec (WSS) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9d14c-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="9d14c-124">integración de hello tooconfigure de Symantec Web seguridad Service (WSS) en Azure AD, deberá tooadd Symantec Web seguridad Service (WSS) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9d14c-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d14c-125">**tooadd Symantec Web seguridad Service (WSS) de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d14c-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d14c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9d14c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d14c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d14c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9d14c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d14c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9d14c-133">En el cuadro de búsqueda de hello, escriba **Symantec Web seguridad Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-133">In hello search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="9d14c-135">En el panel de resultados de hello, seleccione **Symantec Web seguridad Service (WSS)**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9d14c-135">In hello results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d14c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d14c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d14c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9d14c-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d14c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el servicio de seguridad Web de Symantec (WSS) es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d14c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="9d14c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el servicio de seguridad Web de Symantec (WSS) debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9d14c-140">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="9d14c-141">En el servicio de seguridad de Web de Symantec (WSS), asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d14c-141">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9d14c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con el servicio de seguridad Web de Symantec (WSS), deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9d14c-142">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9d14c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9d14c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9d14c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d14c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d14c-145">**[Crear un usuario de prueba de servicio de seguridad de Web (WSS) de Symantec](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave un equivalente de Britta Simon en Symantec Web seguridad Service (WSS) que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9d14c-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d14c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9d14c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d14c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9d14c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d14c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d14c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d14c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de servicio de seguridad de Web (WSS) de Symantec.</span><span class="sxs-lookup"><span data-stu-id="9d14c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="9d14c-150">**tooconfigure inicio de sesión único en Azure AD con el servicio de seguridad de Web de Symantec (WSS), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d14c-150">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="9d14c-151">En el portal de Azure, en Hola Hola **Symantec Web seguridad Service (WSS)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-151">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9d14c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9d14c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="9d14c-155">En hello **dominio del servicio (WSS) de seguridad de Web de Symantec y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9d14c-155">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="9d14c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9d14c-157">a.</span></span> <span data-ttu-id="9d14c-158">Hola **dirección URL de inicio de sesión** cuadro de texto dirección url de hello mención, que desee tooblock según la directiva de bloqueo de toohello de hello Symantec Web seguridad Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9d14c-158">In hello **Sign-on URL** textbox, mention hello url, which you want tooblock according toohello blocking policy of hello Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="9d14c-159">b.</span><span class="sxs-lookup"><span data-stu-id="9d14c-159">b.</span></span> <span data-ttu-id="9d14c-160">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="9d14c-160">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d14c-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9d14c-161">These values are not real.</span></span> <span data-ttu-id="9d14c-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="9d14c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9d14c-163">Póngase en contacto con [equipo de soporte técnico de cliente de servicio de seguridad de Web (WSS) de Symantec](https://www.symantec.com/contact-us) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9d14c-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="9d14c-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9d14c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="9d14c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9d14c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d14c-168">tooconfigure inicio de sesión único en **Symantec Web seguridad Service (WSS)** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipodesoportetécnicodeSymantecWebseguridadService(WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="9d14c-168">tooconfigure single sign-on on **Symantec Web Security Service (WSS)** side, you need toosend hello downloaded **Metadata XML** too[Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="9d14c-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9d14c-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9d14c-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9d14c-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9d14c-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d14c-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d14c-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d14c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d14c-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9d14c-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9d14c-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d14c-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d14c-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9d14c-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d14c-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d14c-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d14c-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d14c-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9d14c-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d14c-184">a.</span><span class="sxs-lookup"><span data-stu-id="9d14c-184">a.</span></span> <span data-ttu-id="9d14c-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d14c-186">b.</span><span class="sxs-lookup"><span data-stu-id="9d14c-186">b.</span></span> <span data-ttu-id="9d14c-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d14c-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d14c-188">c.</span><span class="sxs-lookup"><span data-stu-id="9d14c-188">c.</span></span> <span data-ttu-id="9d14c-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9d14c-190">d.</span><span class="sxs-lookup"><span data-stu-id="9d14c-190">d.</span></span> <span data-ttu-id="9d14c-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="9d14c-192">Crear un usuario de prueba de Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="9d14c-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="9d14c-193">En esta sección, creará un usuario llamado Britta Simon en Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9d14c-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="9d14c-194">Trabajar con [equipo de soporte técnico de Symantec Web seguridad Service (WSS)](https://www.symantec.com/contact-us) para agregar usuarios de hello en plataforma de hello Symantec Web seguridad Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9d14c-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add hello users in hello Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="9d14c-195">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9d14c-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="9d14c-196">También junto con hello usuario informa necesita toosend Hola dirección IP pública de máquina de Hola desde el que está tratando de aplicación de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="9d14c-196">Also along with hello user details you need toosend hello public IPaddress of hello machine from which you are trying tooaccess hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="9d14c-197">Por favor, [haga clic aquí](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget su equipo público de dirección IP.</span><span class="sxs-lookup"><span data-stu-id="9d14c-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9d14c-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d14c-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9d14c-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSymantec Web seguridad Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9d14c-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9d14c-201">**tooassign Britta Simon tooSymantec Web seguridad Service (WSS), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9d14c-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="9d14c-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9d14c-204">En la lista de aplicaciones de hello, seleccione **Symantec Web seguridad Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-204">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="9d14c-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9d14c-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-208">Click **Add** button.</span></span> <span data-ttu-id="9d14c-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9d14c-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d14c-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9d14c-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d14c-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9d14c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d14c-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9d14c-214">Testing single sign-on</span></span>

<span data-ttu-id="9d14c-215">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9d14c-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9d14c-216">Al hacer clic en hello Symantec Web seguridad Service (WSS) el icono Hola Panel de acceso, obtendrá redirigida toohello bloqueo de página para el que se ha configurado la directiva de bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d14c-216">When you click hello Symantec Web Security Service (WSS) tile in hello Access Panel, you get redirected toohello blocking page for which hello blocking policy has been configured.</span></span>
<span data-ttu-id="9d14c-217">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d14c-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d14c-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9d14c-218">Additional resources</span></span>

* [<span data-ttu-id="9d14c-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d14c-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d14c-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d14c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

