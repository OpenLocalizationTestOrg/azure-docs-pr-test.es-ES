---
title: "Tutorial: Integración de Azure Active Directory con BenefitHub | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="6957d-103">Tutorial: Integración de Azure Active Directory con BenefitHub</span><span class="sxs-lookup"><span data-stu-id="6957d-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="6957d-104">En este tutorial, aprenderá cómo toointegrate BenefitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6957d-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6957d-105">Integración BenefitHub con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6957d-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6957d-106">Puede controlar en Azure AD que tenga acceso tooBenefitHub</span><span class="sxs-lookup"><span data-stu-id="6957d-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="6957d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBenefitHub (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6957d-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6957d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6957d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6957d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6957d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6957d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6957d-110">Prerequisites</span></span>

<span data-ttu-id="6957d-111">integración de Azure AD con BenefitHub tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6957d-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="6957d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6957d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6957d-113">Una suscripción habilitada para el inicio de sesión único en BenefitHub</span><span class="sxs-lookup"><span data-stu-id="6957d-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6957d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6957d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6957d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6957d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6957d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6957d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6957d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6957d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6957d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6957d-118">Scenario description</span></span>
<span data-ttu-id="6957d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6957d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6957d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="6957d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6957d-121">Agregar BenefitHub desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6957d-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="6957d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6957d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="6957d-123">Agregar BenefitHub desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6957d-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="6957d-124">integración de hello tooconfigure de BenefitHub en Azure AD, deberá tooadd BenefitHub de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6957d-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6957d-125">**tooadd BenefitHub de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6957d-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6957d-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6957d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6957d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6957d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6957d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6957d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6957d-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6957d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6957d-133">En el cuadro de búsqueda de hello, escriba **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="6957d-133">In hello search box, type **BenefitHub**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="6957d-135">En el panel de resultados de hello, seleccione **BenefitHub**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6957d-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6957d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6957d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6957d-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BenefitHub con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6957d-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6957d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en BenefitHub es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6957d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="6957d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en BenefitHub debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="6957d-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="6957d-141">En BenefitHub, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6957d-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6957d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con BenefitHub, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6957d-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6957d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6957d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6957d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6957d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6957d-145">**[Crear un usuario de prueba BenefitHub](#creating-a-benefithub-test-user)**  -toohave un equivalente de Britta Simon en BenefitHub que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="6957d-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6957d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6957d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6957d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6957d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6957d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6957d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6957d-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="6957d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="6957d-150">**inicio de sesión único en Azure AD tooconfigure con BenefitHub, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6957d-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="6957d-151">En el portal de Azure, en Hola Hola **BenefitHub** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6957d-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6957d-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6957d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="6957d-155">En hello **BenefitHub dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6957d-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="6957d-157">a.</span><span class="sxs-lookup"><span data-stu-id="6957d-157">a.</span></span> <span data-ttu-id="6957d-158">Hola **identificador** cuadro de texto, tipo:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="6957d-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="6957d-159">b.</span><span class="sxs-lookup"><span data-stu-id="6957d-159">b.</span></span> <span data-ttu-id="6957d-160">Hola **dirección URL de respuesta** cuadro de texto, tipo:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="6957d-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="6957d-161">Hola BenefitHub aplicación espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="6957d-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="6957d-162">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="6957d-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="6957d-163">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6957d-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="6957d-165">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en hello delante de la imagen y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6957d-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6957d-166">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="6957d-166">Attribute Name</span></span> | <span data-ttu-id="6957d-167">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="6957d-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6957d-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="6957d-168">organizationid</span></span> | <span data-ttu-id="6957d-169">< identificador de organización ></span><span class="sxs-lookup"><span data-stu-id="6957d-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="6957d-170">Este valor de atributo no es real.</span><span class="sxs-lookup"><span data-stu-id="6957d-170">This attribute value is not real.</span></span> <span data-ttu-id="6957d-171">Actualícelo con el identificador de organización real.</span><span class="sxs-lookup"><span data-stu-id="6957d-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="6957d-172">Póngase en contacto con [equipo de soporte técnico de BenefitHub](https://www.benefithub.com/Home/ContactUs) tooget Hola organizationid real.</span><span class="sxs-lookup"><span data-stu-id="6957d-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="6957d-173">a.</span><span class="sxs-lookup"><span data-stu-id="6957d-173">a.</span></span> <span data-ttu-id="6957d-174">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6957d-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6957d-177">b.</span><span class="sxs-lookup"><span data-stu-id="6957d-177">b.</span></span> <span data-ttu-id="6957d-178">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="6957d-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="6957d-179">c.</span><span class="sxs-lookup"><span data-stu-id="6957d-179">c.</span></span> <span data-ttu-id="6957d-180">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="6957d-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6957d-181">d.</span><span class="sxs-lookup"><span data-stu-id="6957d-181">d.</span></span> <span data-ttu-id="6957d-182">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6957d-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6957d-183">Para poder configurar la aserción de SAML de hello, necesita toocontact su [BenefitHub compatibilidad](https://www.benefithub.com/Home/ContactUs) y solicite el valor de Hola de atributo del identificador único de hello para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="6957d-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="6957d-184">Necesita esta notificación personalizada de valor tooconfigure hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6957d-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="6957d-185">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6957d-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="6957d-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6957d-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6957d-189">tooconfigure inicio de sesión único en **BenefitHub** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="6957d-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="6957d-190">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="6957d-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6957d-191">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="6957d-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6957d-192">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="6957d-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6957d-193">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6957d-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6957d-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6957d-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="6957d-195">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="6957d-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6957d-197">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6957d-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6957d-198">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6957d-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6957d-200">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6957d-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6957d-202">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6957d-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6957d-204">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="6957d-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6957d-206">a.</span><span class="sxs-lookup"><span data-stu-id="6957d-206">a.</span></span> <span data-ttu-id="6957d-207">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6957d-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6957d-208">b.</span><span class="sxs-lookup"><span data-stu-id="6957d-208">b.</span></span> <span data-ttu-id="6957d-209">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6957d-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6957d-210">c.</span><span class="sxs-lookup"><span data-stu-id="6957d-210">c.</span></span> <span data-ttu-id="6957d-211">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6957d-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6957d-212">d.</span><span class="sxs-lookup"><span data-stu-id="6957d-212">d.</span></span> <span data-ttu-id="6957d-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6957d-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="6957d-214">Creación de un usuario de prueba de BenefitHub</span><span class="sxs-lookup"><span data-stu-id="6957d-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="6957d-215">En esta sección, creará un usuario llamado Britta Simon en BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="6957d-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="6957d-216">Trabajar con [equipo de soporte técnico de BenefitHub](https://www.benefithub.com/Home/ContactUs) para agregar usuarios de hello en la plataforma de BenefitHub Hola.</span><span class="sxs-lookup"><span data-stu-id="6957d-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="6957d-217">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6957d-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6957d-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6957d-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6957d-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBenefitHub.</span><span class="sxs-lookup"><span data-stu-id="6957d-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6957d-221">**tooassign Britta Simon tooBenefitHub, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6957d-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="6957d-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6957d-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6957d-224">En la lista de aplicaciones de hello, seleccione **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="6957d-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="6957d-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6957d-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6957d-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6957d-228">Click **Add** button.</span></span> <span data-ttu-id="6957d-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6957d-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6957d-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6957d-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6957d-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6957d-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6957d-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6957d-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6957d-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6957d-234">Testing single sign-on</span></span>

<span data-ttu-id="6957d-235">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6957d-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6957d-236">Al hacer clic en icono de BenefitHub Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour BenefitHub aplicación.</span><span class="sxs-lookup"><span data-stu-id="6957d-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="6957d-237">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="6957d-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6957d-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6957d-238">Additional resources</span></span>

* [<span data-ttu-id="6957d-239">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6957d-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6957d-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6957d-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

