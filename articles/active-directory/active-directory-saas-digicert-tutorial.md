---
title: "Tutorial: integración de Azure Active Directory con DigiCert | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 861039d00533b3aeb361d04e45c4460c6fc8cef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="088a7-103">Tutorial: integración de Azure Active Directory con DigiCert</span><span class="sxs-lookup"><span data-stu-id="088a7-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="088a7-104">En este tutorial, aprenderá cómo toointegrate DigiCert con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="088a7-104">In this tutorial, you learn how toointegrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="088a7-105">Integración DigiCert con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="088a7-105">Integrating DigiCert with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="088a7-106">Puede controlar en Azure AD que tenga acceso tooDigiCert</span><span class="sxs-lookup"><span data-stu-id="088a7-106">You can control in Azure AD who has access tooDigiCert</span></span>
- <span data-ttu-id="088a7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDigiCert (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="088a7-107">You can enable your users tooautomatically get signed-on tooDigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="088a7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="088a7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="088a7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="088a7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="088a7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="088a7-110">Prerequisites</span></span>

<span data-ttu-id="088a7-111">integración de Azure AD con DigiCert tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="088a7-111">tooconfigure Azure AD integration with DigiCert, you need hello following items:</span></span>

- <span data-ttu-id="088a7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="088a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="088a7-113">Una suscripción habilitada para el inicio de sesión único en DigiCert</span><span class="sxs-lookup"><span data-stu-id="088a7-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="088a7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="088a7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="088a7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="088a7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="088a7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="088a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="088a7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="088a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="088a7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="088a7-118">Scenario description</span></span>
<span data-ttu-id="088a7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="088a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="088a7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="088a7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="088a7-121">Agregar DigiCert desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="088a7-121">Adding DigiCert from hello gallery</span></span>
2. <span data-ttu-id="088a7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="088a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-hello-gallery"></a><span data-ttu-id="088a7-123">Agregar DigiCert desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="088a7-123">Adding DigiCert from hello gallery</span></span>
<span data-ttu-id="088a7-124">integración de hello tooconfigure de DigiCert en Azure AD, deberá tooadd DigiCert de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="088a7-124">tooconfigure hello integration of DigiCert into Azure AD, you need tooadd DigiCert from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="088a7-125">**tooadd DigiCert de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="088a7-125">**tooadd DigiCert from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="088a7-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="088a7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="088a7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="088a7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="088a7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="088a7-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="088a7-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="088a7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="088a7-133">En el cuadro de búsqueda de hello, escriba **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="088a7-133">In hello search box, type **DigiCert**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="088a7-135">En el panel de resultados de hello, seleccione **DigiCert**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="088a7-135">In hello results panel, select **DigiCert**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="088a7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="088a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="088a7-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con DigiCert con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="088a7-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="088a7-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en DigiCert es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="088a7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DigiCert is tooa user in Azure AD.</span></span> <span data-ttu-id="088a7-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en DigiCert debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="088a7-140">In other words, a link relationship between an Azure AD user and hello related user in DigiCert needs toobe established.</span></span>

<span data-ttu-id="088a7-141">En DigiCert, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="088a7-141">In DigiCert, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="088a7-142">tooconfigure y prueba de inicio de sesión único en Azure AD con DigiCert, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="088a7-142">tooconfigure and test Azure AD single sign-on with DigiCert, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="088a7-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="088a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="088a7-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="088a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="088a7-145">**[Crear un usuario de prueba de DigiCert](#creating-a-digicert-test-user)**  -toohave un equivalente de Britta Simon en DigiCert que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="088a7-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - toohave a counterpart of Britta Simon in DigiCert that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="088a7-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="088a7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="088a7-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="088a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="088a7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="088a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="088a7-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de DigiCert.</span><span class="sxs-lookup"><span data-stu-id="088a7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="088a7-150">**inicio de sesión único en Azure AD tooconfigure con DigiCert, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="088a7-150">**tooconfigure Azure AD single sign-on with DigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="088a7-151">En el portal de Azure, en Hola Hola **DigiCert** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="088a7-151">In hello Azure portal, on hello **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="088a7-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="088a7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="088a7-155">En hello **DigiCert dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="088a7-155">On hello **DigiCert Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="088a7-157">Aplicación de DigiCert espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="088a7-157">DigiCert application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="088a7-158">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="088a7-158">Configure hello following claims for this application.</span></span> <span data-ttu-id="088a7-159">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="088a7-159">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="088a7-160">Hola siguiente captura de pantalla muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="088a7-160">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="088a7-162">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="088a7-162">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="088a7-163">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="088a7-163">Attribute Name</span></span> | <span data-ttu-id="088a7-164">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="088a7-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="088a7-165">company</span><span class="sxs-lookup"><span data-stu-id="088a7-165">company</span></span> | <span data-ttu-id="088a7-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="088a7-166">< companycode ></span></span> |
    | <span data-ttu-id="088a7-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="088a7-167">digicertrole</span></span> | <span data-ttu-id="088a7-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="088a7-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="088a7-169">Hola valo **empresa** atributo no es real.</span><span class="sxs-lookup"><span data-stu-id="088a7-169">hello value of **company** attribute is not real.</span></span> <span data-ttu-id="088a7-170">Actualícelo con el código real de la empresa.</span><span class="sxs-lookup"><span data-stu-id="088a7-170">Update this value with actual company code.</span></span> <span data-ttu-id="088a7-171">valor de hello tooget de **empresa** póngase en contacto con el atributo [equipo de soporte técnico de DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="088a7-171">tooget hello value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="088a7-172">a.</span><span class="sxs-lookup"><span data-stu-id="088a7-172">a.</span></span> <span data-ttu-id="088a7-173">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="088a7-173">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="088a7-176">b.</span><span class="sxs-lookup"><span data-stu-id="088a7-176">b.</span></span> <span data-ttu-id="088a7-177">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="088a7-177">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="088a7-178">c.</span><span class="sxs-lookup"><span data-stu-id="088a7-178">c.</span></span> <span data-ttu-id="088a7-179">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="088a7-179">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="088a7-180">d.</span><span class="sxs-lookup"><span data-stu-id="088a7-180">d.</span></span> <span data-ttu-id="088a7-181">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="088a7-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="088a7-182">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="088a7-182">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="088a7-184">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="088a7-184">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="088a7-186">tooconfigure inicio de sesión único en **DigiCert** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="088a7-186">tooconfigure single sign-on on **DigiCert** side, you need toosend hello downloaded **Metadata XML** too[DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="088a7-187">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="088a7-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="088a7-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="088a7-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="088a7-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="088a7-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="088a7-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="088a7-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="088a7-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="088a7-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="088a7-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="088a7-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="088a7-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="088a7-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="088a7-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="088a7-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="088a7-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="088a7-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="088a7-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="088a7-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="088a7-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="088a7-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="088a7-203">a.</span><span class="sxs-lookup"><span data-stu-id="088a7-203">a.</span></span> <span data-ttu-id="088a7-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="088a7-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="088a7-205">b.</span><span class="sxs-lookup"><span data-stu-id="088a7-205">b.</span></span> <span data-ttu-id="088a7-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="088a7-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="088a7-207">c.</span><span class="sxs-lookup"><span data-stu-id="088a7-207">c.</span></span> <span data-ttu-id="088a7-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="088a7-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="088a7-209">d.</span><span class="sxs-lookup"><span data-stu-id="088a7-209">d.</span></span> <span data-ttu-id="088a7-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="088a7-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="088a7-211">Creación de un usuario de prueba de DigiCert</span><span class="sxs-lookup"><span data-stu-id="088a7-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="088a7-212">En esta sección, creará un usuario llamado Britta Simon en DigiCert.</span><span class="sxs-lookup"><span data-stu-id="088a7-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="088a7-213">Trabaje con [equipo de soporte técnico de DigiCert](mailto:support@digicert.com) a los usuarios de tooadd hello en DigiCert.</span><span class="sxs-lookup"><span data-stu-id="088a7-213">Please work with [DigiCert support team](mailto:support@digicert.com) tooadd hello users in DigiCert.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="088a7-214">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="088a7-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="088a7-215">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDigiCert.</span><span class="sxs-lookup"><span data-stu-id="088a7-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDigiCert.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="088a7-217">**tooassign Britta Simon tooDigiCert, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="088a7-217">**tooassign Britta Simon tooDigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="088a7-218">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="088a7-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="088a7-220">En la lista de aplicaciones de hello, seleccione **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="088a7-220">In hello applications list, select **DigiCert**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="088a7-222">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="088a7-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="088a7-224">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="088a7-224">Click **Add** button.</span></span> <span data-ttu-id="088a7-225">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="088a7-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="088a7-227">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="088a7-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="088a7-228">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="088a7-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="088a7-229">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="088a7-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="088a7-230">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="088a7-230">Testing single sign-on</span></span>

<span data-ttu-id="088a7-231">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="088a7-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="088a7-232">Al hacer clic en icono de DigiCert Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour DeigiCert aplicación.</span><span class="sxs-lookup"><span data-stu-id="088a7-232">When you click hello DigiCert tile in hello Access Panel, you should get automatically signed-on tooyour DeigiCert application.</span></span>
<span data-ttu-id="088a7-233">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="088a7-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="088a7-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="088a7-234">Additional resources</span></span>

* [<span data-ttu-id="088a7-235">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="088a7-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="088a7-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="088a7-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

