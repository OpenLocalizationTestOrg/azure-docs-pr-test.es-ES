---
title: "Tutorial: Integración de Azure Active Directory con iLMS | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="c51fd-103">Tutorial: Integración de Azure Active Directory con iLMS</span><span class="sxs-lookup"><span data-stu-id="c51fd-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="c51fd-104">En este tutorial, aprenderá cómo toointegrate iLMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c51fd-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c51fd-105">Integración iLMS con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c51fd-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c51fd-106">Puede controlar en Azure AD que tenga acceso tooiLMS</span><span class="sxs-lookup"><span data-stu-id="c51fd-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="c51fd-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooiLMS (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51fd-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c51fd-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c51fd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c51fd-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c51fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c51fd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c51fd-110">Prerequisites</span></span>

<span data-ttu-id="c51fd-111">integración de Azure AD con iLMS tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c51fd-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="c51fd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c51fd-113">Una suscripción habilitada para inicio de sesión único en iLMS</span><span class="sxs-lookup"><span data-stu-id="c51fd-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c51fd-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c51fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c51fd-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c51fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c51fd-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c51fd-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c51fd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c51fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c51fd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c51fd-118">Scenario description</span></span>
<span data-ttu-id="c51fd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c51fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c51fd-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c51fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c51fd-121">Agregar iLMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c51fd-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="c51fd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="c51fd-123">Agregar iLMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c51fd-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="c51fd-124">integración de hello tooconfigure de iLMS en Azure AD, deberá tooadd iLMS de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c51fd-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c51fd-125">**tooadd iLMS de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51fd-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51fd-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c51fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c51fd-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c51fd-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c51fd-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51fd-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c51fd-133">En el cuadro de búsqueda de hello, escriba **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-133">In hello search box, type **iLMS**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="c51fd-135">En el panel de resultados de hello, seleccione **iLMS**, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c51fd-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c51fd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c51fd-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con iLMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c51fd-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c51fd-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en iLMS es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c51fd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="c51fd-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en iLMS debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c51fd-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="c51fd-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en iLMS.</span><span class="sxs-lookup"><span data-stu-id="c51fd-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="c51fd-142">tooconfigure y prueba de inicio de sesión único en Azure AD con iLMS, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c51fd-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c51fd-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c51fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c51fd-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c51fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c51fd-145">**[Creación de un usuario de prueba iLMS](#creating-an-ilms-test-user) ** -toohave un equivalente de Britta Simon en iLMS que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="c51fd-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c51fd-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c51fd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c51fd-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c51fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c51fd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c51fd-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación iLMS.</span><span class="sxs-lookup"><span data-stu-id="c51fd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="c51fd-150">**inicio de sesión único en Azure AD tooconfigure con iLMS, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51fd-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51fd-151">En el portal de Azure, en Hola Hola **iLMS** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c51fd-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c51fd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="c51fd-155">En hello **iLMS dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="c51fd-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="c51fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="c51fd-157">a.</span></span> <span data-ttu-id="c51fd-158">Hola **identificador** cuadro de texto, pegue hello **identificador** valor copiar de **proveedor de servicios** sección de configuración de SAML en el portal de administración de iLMS.</span><span class="sxs-lookup"><span data-stu-id="c51fd-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="c51fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="c51fd-159">b.</span></span> <span data-ttu-id="c51fd-160">Hola **dirección URL de respuesta** cuadro de texto, pegue hello **(dirección URL del extremo)** valor copiar de **proveedor de servicios** sección de configuración de SAML en el portal de administración de iLMS tener siguiente Hola patrón`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="c51fd-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="c51fd-161">"123456" es un valor de ejemplo del identificador.</span><span class="sxs-lookup"><span data-stu-id="c51fd-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="c51fd-162">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="c51fd-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="c51fd-164">Hola **dirección URL de inicio de sesión** cuadro de texto, pegue hello **(dirección URL del extremo)** valor copiar de **proveedor de servicios** sección de configuración de SAML en el portal de administración de iLMS como`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="c51fd-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="c51fd-165">tooenable JIT aprovisionamiento, iLMS aplicación espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="c51fd-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c51fd-166">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="c51fd-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="c51fd-167">Puede administrar valores de hello de estos atributos de hello **atributos de usuario** sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c51fd-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="c51fd-168">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="c51fd-168">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="c51fd-170">Crear **departamento, región** y **división** atributos y agregue el nombre de Hola de estos atributos en iLMS.</span><span class="sxs-lookup"><span data-stu-id="c51fd-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="c51fd-171">Todos estos atributos mostrados anteriormente son obligatorios.</span><span class="sxs-lookup"><span data-stu-id="c51fd-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="c51fd-172">Tiene tooenable **crear cuenta de usuario de Un-recognized** en iLMS toomap estos atributos.</span><span class="sxs-lookup"><span data-stu-id="c51fd-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="c51fd-173">Siga las instrucciones de hello [aquí](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget una idea en la configuración de atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51fd-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="c51fd-174">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c51fd-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c51fd-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="c51fd-175">Attribute Name</span></span> | <span data-ttu-id="c51fd-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="c51fd-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="c51fd-177">division</span><span class="sxs-lookup"><span data-stu-id="c51fd-177">division</span></span> | <span data-ttu-id="c51fd-178">user.department</span><span class="sxs-lookup"><span data-stu-id="c51fd-178">user.department</span></span> |
    | <span data-ttu-id="c51fd-179">region</span><span class="sxs-lookup"><span data-stu-id="c51fd-179">region</span></span> | <span data-ttu-id="c51fd-180">user.state</span><span class="sxs-lookup"><span data-stu-id="c51fd-180">user.state</span></span> |
    | <span data-ttu-id="c51fd-181">department</span><span class="sxs-lookup"><span data-stu-id="c51fd-181">department</span></span> | <span data-ttu-id="c51fd-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="c51fd-182">user.jobtitle</span></span> |

    <span data-ttu-id="c51fd-183">a.</span><span class="sxs-lookup"><span data-stu-id="c51fd-183">a.</span></span> <span data-ttu-id="c51fd-184">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c51fd-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="c51fd-187">b.</span><span class="sxs-lookup"><span data-stu-id="c51fd-187">b.</span></span> <span data-ttu-id="c51fd-188">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="c51fd-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c51fd-189">c.</span><span class="sxs-lookup"><span data-stu-id="c51fd-189">c.</span></span> <span data-ttu-id="c51fd-190">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="c51fd-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c51fd-191">d.</span><span class="sxs-lookup"><span data-stu-id="c51fd-191">d.</span></span> <span data-ttu-id="c51fd-192">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-192">Click **Ok**</span></span>

7. <span data-ttu-id="c51fd-193">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c51fd-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="c51fd-195">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c51fd-195">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="c51fd-197">En una ventana del explorador web diferente, inicie sesión en tooyour **portal de administración de iLMS** como administrador.</span><span class="sxs-lookup"><span data-stu-id="c51fd-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="c51fd-198">Haga clic en **SSO:SAML** en **configuración** ficha Configuración de SAML tooopen y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c51fd-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="c51fd-200">a.</span><span class="sxs-lookup"><span data-stu-id="c51fd-200">a.</span></span> <span data-ttu-id="c51fd-201">Expanda hello **proveedor de servicios** sección y copia hello **identificador** y **(dirección URL del extremo)** valor.</span><span class="sxs-lookup"><span data-stu-id="c51fd-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="c51fd-203">b.</span><span class="sxs-lookup"><span data-stu-id="c51fd-203">b.</span></span> <span data-ttu-id="c51fd-204">En la sección **Identity Provider** (Proveedor de identidades), haga clic en **Import Metadata** (Importar metadatos).</span><span class="sxs-lookup"><span data-stu-id="c51fd-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="c51fd-205">c.</span><span class="sxs-lookup"><span data-stu-id="c51fd-205">c.</span></span> <span data-ttu-id="c51fd-206">Seleccione hello **metadatos** archivo descargado desde el Portal de Azure desde **el certificado de firma de SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="c51fd-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="c51fd-208">d.</span><span class="sxs-lookup"><span data-stu-id="c51fd-208">d.</span></span> <span data-ttu-id="c51fd-209">Si desea que tooenable JIT aprovisionamiento toocreate iLMS de cuentas para anular-reconocer a los usuarios, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c51fd-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="c51fd-210">Active **Create Un-recognized User Account** (Crear cuenta de usuario no reconocido).</span><span class="sxs-lookup"><span data-stu-id="c51fd-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="c51fd-212">Asignar atributos de hello en Azure AD con atributos de hello en iLMS.</span><span class="sxs-lookup"><span data-stu-id="c51fd-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="c51fd-213">En la columna de atributos de hello, especifique el valor de predeterminada de nombre o hello de atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51fd-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="c51fd-214">e.</span><span class="sxs-lookup"><span data-stu-id="c51fd-214">e.</span></span> <span data-ttu-id="c51fd-215">Vaya demasiado**reglas de negocios** pestaña y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c51fd-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="c51fd-217">Comprobar **crear Un-recognized regiones, divisiones y departamentos** toocreate regiones, divisiones y departamentos que ya no existen en tiempo de Hola de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c51fd-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="c51fd-218">Comprobar **actualizar el perfil de usuario durante inicio de sesión de** toospecify si se actualiza el perfil de usuario de hello con cada inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c51fd-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="c51fd-219">Si hello **"Actualización en blanco valores para no campos en el perfil de usuario obligatorio"** opción está activada, campos de perfil opcional que están en blanco al inicio de sesión será también provocar hello iLMS perfil usuario toocontain valores en blanco para esos campos.</span><span class="sxs-lookup"><span data-stu-id="c51fd-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="c51fd-220">Comprobar **enviar correo electrónico de notificación de Error** y escriba correo electrónico de saludo del usuario de Hola donde desea que el correo electrónico de notificación de error de tooreceive Hola.</span><span class="sxs-lookup"><span data-stu-id="c51fd-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="c51fd-221">Haga clic en **guardar** botón Configuración de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="c51fd-221">Click **Save** button toosave hello settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="c51fd-223">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c51fd-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c51fd-224">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c51fd-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c51fd-225">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c51fd-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c51fd-226">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51fd-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="c51fd-227">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c51fd-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c51fd-229">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51fd-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51fd-230">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c51fd-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c51fd-232">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c51fd-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c51fd-234">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c51fd-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c51fd-236">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c51fd-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c51fd-238">a.</span><span class="sxs-lookup"><span data-stu-id="c51fd-238">a.</span></span> <span data-ttu-id="c51fd-239">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c51fd-240">b.</span><span class="sxs-lookup"><span data-stu-id="c51fd-240">b.</span></span> <span data-ttu-id="c51fd-241">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c51fd-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c51fd-242">c.</span><span class="sxs-lookup"><span data-stu-id="c51fd-242">c.</span></span> <span data-ttu-id="c51fd-243">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c51fd-244">d.</span><span class="sxs-lookup"><span data-stu-id="c51fd-244">d.</span></span> <span data-ttu-id="c51fd-245">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="c51fd-246">Creación de un usuario de prueba de iLMS</span><span class="sxs-lookup"><span data-stu-id="c51fd-246">Creating an iLMS test user</span></span>

<span data-ttu-id="c51fd-247">Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de autenticar usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c51fd-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="c51fd-248">JIT funcionará, si ha seleccionado hello **crear cuenta de usuario de Un-recognized** casilla durante la configuración de SAML en el portal de administración de iLMS.</span><span class="sxs-lookup"><span data-stu-id="c51fd-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="c51fd-249">Si necesita un usuario toocreate manualmente, siga pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c51fd-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="c51fd-250">Inicie sesión en el sitio de la empresa iLMS tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="c51fd-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="c51fd-251">Haga clic en **"Registrar usuario"** en **usuarios** ficha tooopen **Registrar usuario** página.</span><span class="sxs-lookup"><span data-stu-id="c51fd-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Agregar empleado](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="c51fd-253">En hello **"Registrar usuario"** , siga los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51fd-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Agregar empleado](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="c51fd-255">a.</span><span class="sxs-lookup"><span data-stu-id="c51fd-255">a.</span></span> <span data-ttu-id="c51fd-256">Hola **nombre** cuadro de texto, tipo hello nombre Bárbara.</span><span class="sxs-lookup"><span data-stu-id="c51fd-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="c51fd-257">b.</span><span class="sxs-lookup"><span data-stu-id="c51fd-257">b.</span></span> <span data-ttu-id="c51fd-258">Hola **Last Name** cuadro de texto, hello tipo apellidos Simon.</span><span class="sxs-lookup"><span data-stu-id="c51fd-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="c51fd-259">c.</span><span class="sxs-lookup"><span data-stu-id="c51fd-259">c.</span></span> <span data-ttu-id="c51fd-260">Hola **Id. de correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c51fd-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="c51fd-261">d.</span><span class="sxs-lookup"><span data-stu-id="c51fd-261">d.</span></span> <span data-ttu-id="c51fd-262">Hola **región** lista desplegable valor seleccione Hola de región.</span><span class="sxs-lookup"><span data-stu-id="c51fd-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="c51fd-263">e.</span><span class="sxs-lookup"><span data-stu-id="c51fd-263">e.</span></span> <span data-ttu-id="c51fd-264">Hola **división** lista desplegable, valor de hello select para la división.</span><span class="sxs-lookup"><span data-stu-id="c51fd-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="c51fd-265">f.</span><span class="sxs-lookup"><span data-stu-id="c51fd-265">f.</span></span> <span data-ttu-id="c51fd-266">Hola **departamento** lista desplegable valor seleccione Hola de departamento.</span><span class="sxs-lookup"><span data-stu-id="c51fd-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="c51fd-267">g.</span><span class="sxs-lookup"><span data-stu-id="c51fd-267">g.</span></span> <span data-ttu-id="c51fd-268">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c51fd-269">Puede enviar toouser de correo electrónico de registro seleccionando **enviar correo de registro** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="c51fd-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c51fd-270">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c51fd-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c51fd-271">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooiLMS de acceso.</span><span class="sxs-lookup"><span data-stu-id="c51fd-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c51fd-273">**tooassign Britta Simon tooiLMS, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c51fd-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="c51fd-274">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c51fd-276">En la lista de aplicaciones de hello, seleccione **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-276">In hello applications list, select **iLMS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="c51fd-278">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c51fd-280">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-280">Click **Add** button.</span></span> <span data-ttu-id="c51fd-281">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c51fd-283">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c51fd-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c51fd-284">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c51fd-285">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c51fd-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c51fd-286">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c51fd-286">Testing single sign-on</span></span>

<span data-ttu-id="c51fd-287">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c51fd-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c51fd-288">Al hacer clic en hello iLMS el icono Panel de acceso de hello, deberá obtener automáticamente ha iniciado sesión tooyour iLMS aplicación.</span><span class="sxs-lookup"><span data-stu-id="c51fd-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c51fd-289">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c51fd-289">Additional resources</span></span>

* [<span data-ttu-id="c51fd-290">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c51fd-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c51fd-291">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c51fd-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

