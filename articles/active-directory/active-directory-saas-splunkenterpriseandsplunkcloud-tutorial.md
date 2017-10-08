---
title: "Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Splunk Enterprise y Splunk en la nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 848e0485131321479f2375501b330c798627e7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="32526-103">Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="32526-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="32526-104">En este tutorial, aprenderá cómo toointegrate Splunk Enterprise y Splunk en la nube con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32526-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32526-105">Integración de Splunk Enterprise y Splunk en la nube con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="32526-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32526-106">Puede controlar en Azure AD que tenga acceso tooSplunk Enterprise y Splunk en la nube</span><span class="sxs-lookup"><span data-stu-id="32526-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="32526-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSplunk Enterprise y Splunk en la nube (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32526-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32526-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="32526-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32526-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32526-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32526-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="32526-110">Prerequisites</span></span>

<span data-ttu-id="32526-111">tooconfigure integración de Azure AD con Splunk Enterprise y Splunk en la nube, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="32526-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="32526-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32526-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32526-113">Una suscripción habilitada para inicio de sesión único en Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="32526-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32526-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="32526-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32526-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="32526-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32526-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="32526-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32526-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32526-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32526-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="32526-118">Scenario description</span></span>
<span data-ttu-id="32526-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="32526-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32526-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="32526-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32526-121">Agregar Splunk Enterprise y Splunk en la nube de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="32526-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="32526-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32526-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="32526-123">Agregar Splunk Enterprise y Splunk en la nube de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="32526-123">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="32526-124">integración de hello tooconfigure de empresa de Splunk y Splunk en la nube en Azure AD, necesita tooadd Splunk Enterprise y Splunk en la nube de lista de tooyour Hola Galería de las aplicaciones de SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="32526-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32526-125">**tooadd Splunk Enterprise y Splunk en la nube de la Galería de hello, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32526-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32526-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="32526-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32526-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="32526-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32526-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="32526-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="32526-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32526-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="32526-133">En el cuadro de búsqueda de hello, escriba **Splunk empresarial y en la nube Splunk**.</span><span class="sxs-lookup"><span data-stu-id="32526-133">In hello search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="32526-135">En el panel de resultados de hello, seleccione **Splunk empresarial y en la nube Splunk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="32526-135">In hello results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32526-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32526-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32526-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Splunk Enterprise y Splunk Cloud mediante un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32526-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32526-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Splunk Enterprise y Splunk en la nube es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32526-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="32526-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Splunk Enterprise y Splunk en la nube debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="32526-140">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="32526-141">En Splunk Enterprise y Splunk en la nube, asignar el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32526-141">In Splunk Enterprise and Splunk Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="32526-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Splunk Enterprise y Splunk en la nube, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="32526-142">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32526-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="32526-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32526-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32526-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32526-145">**[Crear un usuario de prueba Splunk empresarial y en la nube Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave un equivalente de Britta Simon de empresa de Splunk y Splunk en la nube que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="32526-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32526-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="32526-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32526-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="32526-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32526-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32526-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32526-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación empresarial de Splunk y Splunk en la nube.</span><span class="sxs-lookup"><span data-stu-id="32526-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="32526-150">**tooconfigure inicio de sesión único en Azure AD con Splunk Enterprise y Splunk en la nube, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32526-150">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="32526-151">En el portal de Azure, en Hola Hola **Splunk empresarial y en la nube Splunk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="32526-151">In hello Azure portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="32526-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="32526-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="32526-155">En hello **Splunk Enterprise y Splunk nube dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="32526-155">On hello **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="32526-157">a.</span><span class="sxs-lookup"><span data-stu-id="32526-157">a.</span></span> <span data-ttu-id="32526-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="32526-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="32526-159">b.</span><span class="sxs-lookup"><span data-stu-id="32526-159">b.</span></span> <span data-ttu-id="32526-160">Hola **identificador** cuadro de texto, escriba Hola la dirección URL del servidor Splunk.</span><span class="sxs-lookup"><span data-stu-id="32526-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>

    <span data-ttu-id="32526-161">c.</span><span class="sxs-lookup"><span data-stu-id="32526-161">c.</span></span> <span data-ttu-id="32526-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="32526-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32526-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="32526-163">These values are not real.</span></span> <span data-ttu-id="32526-164">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="32526-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="32526-165">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="32526-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="32526-166">Póngase en contacto con [equipo de soporte técnico Splunk empresarial y el cliente de la nube de Splunk](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="32526-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget these values.</span></span> 

4. <span data-ttu-id="32526-167">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="32526-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="32526-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="32526-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32526-171">tooconfigure inicio de sesión único en **Splunk empresarial y en la nube Splunk** lado, necesita hello toosend descargado **Metadata XML** demasiado[Splunk empresarial y en la nube Splunk equipodesoporte](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="32526-171">tooconfigure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need toosend hello downloaded **Metadata XML** too[Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="32526-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="32526-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32526-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="32526-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32526-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32526-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32526-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32526-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="32526-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="32526-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="32526-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32526-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32526-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="32526-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32526-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="32526-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32526-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32526-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32526-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="32526-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32526-187">a.</span><span class="sxs-lookup"><span data-stu-id="32526-187">a.</span></span> <span data-ttu-id="32526-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32526-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32526-189">b.</span><span class="sxs-lookup"><span data-stu-id="32526-189">b.</span></span> <span data-ttu-id="32526-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32526-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32526-191">c.</span><span class="sxs-lookup"><span data-stu-id="32526-191">c.</span></span> <span data-ttu-id="32526-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="32526-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32526-193">d.</span><span class="sxs-lookup"><span data-stu-id="32526-193">d.</span></span> <span data-ttu-id="32526-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="32526-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="32526-195">Creación de un usuario de prueba de Splunk Enterprise y Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="32526-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="32526-196">En esta sección, creará un usuario llamado Britta Simon en Splunk Enterprise y Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="32526-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="32526-197">Trabajar con [equipo de soporte técnico Splunk empresarial y en la nube Splunk](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) a los usuarios de tooadd hello en hello Splunk Enterprise y plataforma de nube Splunk.</span><span class="sxs-lookup"><span data-stu-id="32526-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32526-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="32526-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32526-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSplunk Enterprise y Splunk en la nube.</span><span class="sxs-lookup"><span data-stu-id="32526-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="32526-201">**tooassign Britta Simon tooSplunk Enterprise y Splunk en la nube, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="32526-201">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="32526-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="32526-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="32526-204">En la lista de aplicaciones de hello, seleccione **Splunk empresarial y en la nube Splunk**.</span><span class="sxs-lookup"><span data-stu-id="32526-204">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="32526-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="32526-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="32526-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="32526-208">Click **Add** button.</span></span> <span data-ttu-id="32526-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="32526-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="32526-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="32526-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32526-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="32526-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32526-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="32526-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32526-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="32526-214">Testing single sign-on</span></span>

<span data-ttu-id="32526-215">En esta sección, probará la AD SSOonfiguration de Azure con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="32526-215">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="32526-216">Al hacer clic en hello Splunk empresarial y el icono de nube Splunk Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación empresarial de Splunk y Splunk en la nube.</span><span class="sxs-lookup"><span data-stu-id="32526-216">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32526-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="32526-217">Additional resources</span></span>

* [<span data-ttu-id="32526-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32526-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32526-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32526-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

