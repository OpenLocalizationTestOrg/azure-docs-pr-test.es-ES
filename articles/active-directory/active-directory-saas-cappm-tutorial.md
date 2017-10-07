---
title: "Tutorial: Integración de Azure Active Directory con CA PPM | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PPM de entidad emisora de certificados."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 571130f3be0529c986aa0d8a08e4172015cd0b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="99d1a-103">Tutorial: Integración de Azure Active Directory con CA PPM</span><span class="sxs-lookup"><span data-stu-id="99d1a-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="99d1a-104">En este tutorial, aprenderá cómo toointegrate PPM de entidad emisora de certificados con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99d1a-104">In this tutorial, you learn how toointegrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99d1a-105">Integrar CA PPM con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="99d1a-105">Integrating CA PPM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="99d1a-106">Puede controlar en Azure AD que tenga acceso tooCA PPM</span><span class="sxs-lookup"><span data-stu-id="99d1a-106">You can control in Azure AD who has access tooCA PPM</span></span>
- <span data-ttu-id="99d1a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCA PPM (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99d1a-107">You can enable your users tooautomatically get signed-on tooCA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="99d1a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="99d1a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="99d1a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99d1a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99d1a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99d1a-110">Prerequisites</span></span>

<span data-ttu-id="99d1a-111">tooconfigure integración de Azure AD con la entidad de certificación PPM, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="99d1a-111">tooconfigure Azure AD integration with CA PPM, you need hello following items:</span></span>

- <span data-ttu-id="99d1a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99d1a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99d1a-113">Una suscripción habilitada para el inicio de sesión único en CA PPM</span><span class="sxs-lookup"><span data-stu-id="99d1a-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="99d1a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="99d1a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="99d1a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="99d1a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99d1a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="99d1a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="99d1a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99d1a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99d1a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="99d1a-118">Scenario description</span></span>
<span data-ttu-id="99d1a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="99d1a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="99d1a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="99d1a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99d1a-121">Agregar entidad de certificación PPM de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="99d1a-121">Adding CA PPM from hello gallery</span></span>
2. <span data-ttu-id="99d1a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99d1a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-hello-gallery"></a><span data-ttu-id="99d1a-123">Agregar entidad de certificación PPM de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="99d1a-123">Adding CA PPM from hello gallery</span></span>
<span data-ttu-id="99d1a-124">integración de hello tooconfigure ppm de entidad emisora de certificados en Azure AD, deberá tooadd PPM de entidad emisora de certificados de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="99d1a-124">tooconfigure hello integration of CA PPM into Azure AD, you need tooadd CA PPM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="99d1a-125">**tooadd PPM de entidad emisora de certificados de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99d1a-125">**tooadd CA PPM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="99d1a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="99d1a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="99d1a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="99d1a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="99d1a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="99d1a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="99d1a-133">En el cuadro de búsqueda de hello, escriba **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-133">In hello search box, type **CA PPM**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="99d1a-135">En el panel de resultados de hello, seleccione **CA PPM**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="99d1a-135">In hello results panel, select **CA PPM**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99d1a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99d1a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99d1a-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con CA PPM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99d1a-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="99d1a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PPM de entidad emisora de certificados es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99d1a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CA PPM is tooa user in Azure AD.</span></span> <span data-ttu-id="99d1a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PPM de CA debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="99d1a-140">In other words, a link relationship between an Azure AD user and hello related user in CA PPM needs toobe established.</span></span>

<span data-ttu-id="99d1a-141">En Canadá PPM, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="99d1a-141">In CA PPM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="99d1a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con CA PPM, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="99d1a-142">tooconfigure and test Azure AD single sign-on with CA PPM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="99d1a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="99d1a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="99d1a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99d1a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99d1a-145">**[Crear un usuario de prueba de la entidad emisora de certificados PPM](#creating-a-ca-ppm-test-user)**  -toohave un equivalente de Britta Simon en PPM de entidad emisora de certificados que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="99d1a-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - toohave a counterpart of Britta Simon in CA PPM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="99d1a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="99d1a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99d1a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="99d1a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99d1a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99d1a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="99d1a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de PPM de entidad emisora de certificados.</span><span class="sxs-lookup"><span data-stu-id="99d1a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="99d1a-150">**inicio de sesión único en tooconfigure Azure AD con la entidad de certificación PPM, realizar Hola siguiendo los pasos:**</span><span class="sxs-lookup"><span data-stu-id="99d1a-150">**tooconfigure Azure AD single sign-on with CA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="99d1a-151">En el portal de Azure, en Hola Hola **CA PPM** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-151">In hello Azure portal, on hello **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="99d1a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="99d1a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="99d1a-155">En hello **CA PPM dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="99d1a-155">On hello **CA PPM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="99d1a-157">a.</span><span class="sxs-lookup"><span data-stu-id="99d1a-157">a.</span></span> <span data-ttu-id="99d1a-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="99d1a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="99d1a-159">b.</span><span class="sxs-lookup"><span data-stu-id="99d1a-159">b.</span></span> <span data-ttu-id="99d1a-160">Hola **dirección URL de respuesta** cuadro de texto, tipo como:`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="99d1a-160">In hello **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="99d1a-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="99d1a-161">This value is not real.</span></span> <span data-ttu-id="99d1a-162">Actualice este valor con hello identificador real.</span><span class="sxs-lookup"><span data-stu-id="99d1a-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="99d1a-163">Póngase en contacto con [equipo de soporte técnico de la entidad emisora de certificados PPM](mailto:catechnicalsupport@ca.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="99d1a-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) tooget this value.</span></span>
 
4. <span data-ttu-id="99d1a-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="99d1a-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="99d1a-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="99d1a-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="99d1a-168">En hello **la configuración de CA PPM** sección, haga clic en **configurar CA PPM** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="99d1a-168">On hello **CA PPM Configuration** section, click **Configure CA PPM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="99d1a-169">Hola copia **Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="99d1a-169">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="99d1a-171">tooconfigure inicio de sesión único en **CA PPM** lado, necesita hello toosend descargado **Certificate(Base64)** y **Id. de entidad SAML** demasiado[equipo de soporte técnico de PPM de entidad emisora de certificados ](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="99d1a-171">tooconfigure single sign-on on **CA PPM** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Entity ID** too[CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="99d1a-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="99d1a-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="99d1a-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="99d1a-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="99d1a-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="99d1a-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99d1a-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99d1a-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="99d1a-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="99d1a-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="99d1a-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99d1a-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="99d1a-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="99d1a-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="99d1a-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="99d1a-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="99d1a-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="99d1a-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="99d1a-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="99d1a-187">a.</span><span class="sxs-lookup"><span data-stu-id="99d1a-187">a.</span></span> <span data-ttu-id="99d1a-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99d1a-189">b.</span><span class="sxs-lookup"><span data-stu-id="99d1a-189">b.</span></span> <span data-ttu-id="99d1a-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="99d1a-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="99d1a-191">c.</span><span class="sxs-lookup"><span data-stu-id="99d1a-191">c.</span></span> <span data-ttu-id="99d1a-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="99d1a-193">d.</span><span class="sxs-lookup"><span data-stu-id="99d1a-193">d.</span></span> <span data-ttu-id="99d1a-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="99d1a-195">Creación de un usuario de prueba de CA PPM</span><span class="sxs-lookup"><span data-stu-id="99d1a-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="99d1a-196">En esta sección, creará un usuario llamado Britta Simon en CA PPM.</span><span class="sxs-lookup"><span data-stu-id="99d1a-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="99d1a-197">Trabajar con [equipo de soporte técnico de la entidad emisora de certificados PPM](mailto:catechnicalsupport@ca.com) a los usuarios de tooadd hello en la plataforma de hello PPM de entidad emisora de certificados.</span><span class="sxs-lookup"><span data-stu-id="99d1a-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) tooadd hello users in hello CA PPM platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="99d1a-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="99d1a-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="99d1a-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCA PPM.</span><span class="sxs-lookup"><span data-stu-id="99d1a-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCA PPM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="99d1a-201">**tooassign Britta Simon tooCA PPM, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99d1a-201">**tooassign Britta Simon tooCA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="99d1a-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="99d1a-204">En la lista de aplicaciones de hello, seleccione **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-204">In hello applications list, select **CA PPM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="99d1a-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="99d1a-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-208">Click **Add** button.</span></span> <span data-ttu-id="99d1a-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="99d1a-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="99d1a-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="99d1a-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="99d1a-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="99d1a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="99d1a-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="99d1a-214">Testing single sign-on</span></span>

<span data-ttu-id="99d1a-215">En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="99d1a-215">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="99d1a-216">Al hacer clic en icono de CA PPM Hola Hola Panel de acceso, deberá obtener aplicaciones de CA PPM tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="99d1a-216">When you click hello CA PPM tile in hello Access Panel, you should get automatically signed-on tooyour CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99d1a-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="99d1a-217">Additional resources</span></span>

* [<span data-ttu-id="99d1a-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99d1a-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99d1a-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99d1a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

