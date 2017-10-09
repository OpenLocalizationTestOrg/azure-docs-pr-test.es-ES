---
title: "Tutorial: Integración de Azure Active Directory con Velpic SAML | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="17208-103">Tutorial: Integración de Azure Active Directory con Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="17208-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="17208-104">En este tutorial, aprenderá cómo toointegrate Velpic SAML con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17208-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17208-105">Integración Velpic SAML con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="17208-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17208-106">Puede controlar en Azure AD que tenga acceso tooVelpic SAML</span><span class="sxs-lookup"><span data-stu-id="17208-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="17208-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooVelpic SAML (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17208-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17208-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="17208-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="17208-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17208-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17208-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="17208-110">Prerequisites</span></span>

<span data-ttu-id="17208-111">tooconfigure integración de Azure AD con Velpic SAML, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="17208-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="17208-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17208-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17208-113">Una suscripción habilitada para el inicio de sesión único en Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="17208-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17208-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="17208-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17208-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="17208-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17208-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="17208-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="17208-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17208-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17208-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="17208-118">Scenario description</span></span>
<span data-ttu-id="17208-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="17208-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17208-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="17208-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17208-121">Agregar Velpic SAML desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="17208-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="17208-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17208-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="17208-123">Agregar Velpic SAML desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="17208-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="17208-124">integración de hello tooconfigure de Velpic SAML en Azure AD, deberá tooadd Velpic SAML en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="17208-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17208-125">**tooadd Velpic SAML de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17208-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17208-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="17208-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17208-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="17208-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17208-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17208-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="17208-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="17208-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="17208-133">En el cuadro de búsqueda de hello, escriba **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="17208-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="17208-135">En el panel de resultados de hello, seleccione **Velpic SAML**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="17208-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17208-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17208-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17208-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Velpic SAML utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="17208-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17208-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Velpic SAML es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17208-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="17208-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Velpic SAML debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="17208-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="17208-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="17208-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="17208-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Velpic SAML, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="17208-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17208-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="17208-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17208-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17208-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17208-145">**[Crear un usuario de prueba Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave un equivalente de Britta Simon en Velpic SAML que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="17208-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="17208-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="17208-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17208-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="17208-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17208-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17208-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17208-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="17208-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="17208-150">**inicio de sesión único en Azure AD tooconfigure con Velpic SAML, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17208-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="17208-151">En el portal de administración de Azure de hello, en hello **Velpic SAML** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="17208-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="17208-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="17208-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="17208-155">Escriba los detalles de Hola Hola **Velpic SAML dominio y las direcciones URL** sección:</span><span class="sxs-lookup"><span data-stu-id="17208-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="17208-157">a.</span><span class="sxs-lookup"><span data-stu-id="17208-157">a.</span></span> <span data-ttu-id="17208-158">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="17208-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="17208-159">b.</span><span class="sxs-lookup"><span data-stu-id="17208-159">b.</span></span> <span data-ttu-id="17208-160">Hola **identificador** cuadro de texto, pegue hello **'Solo la dirección URL de inicio de sesión'** valor`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="17208-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="17208-161">Tenga en cuenta que Hola equipo Velpic SAML proporcionarán Hola dirección URL de inicio de sesión y el valor de identificador estarán disponible al configurar Hola complemento SSO en el lado de Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="17208-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="17208-162">Debe toocopy que valor de página de la aplicación Velpic SAML y péguelo aquí.</span><span class="sxs-lookup"><span data-stu-id="17208-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="17208-163">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="17208-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="17208-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="17208-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17208-167">En la sección de configuración de SAML Velpic hello, haga clic en configurar Velpic SAML tooopen configurar inicio de sesión en la ventana.</span><span class="sxs-lookup"><span data-stu-id="17208-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="17208-168">Copie Hola Id. de entidad de SAML de hello sección de referencia rápida.</span><span class="sxs-lookup"><span data-stu-id="17208-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="17208-169">En otra ventana del explorador web, inicie sesión como administrador en su sitio de la compañía de Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="17208-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="17208-170">Haga clic en **administrar** pestaña e ir demasiado**integración** sección donde se necesitan tooclick en **complementos** botón toocreate nuevo complemento para el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="17208-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="17208-172">Haga clic en hello **'Agregar complemento'** botón.</span><span class="sxs-lookup"><span data-stu-id="17208-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="17208-174">Haga clic en hello **SAML** disponer en mosaico en la página Agregar complemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="17208-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="17208-176">Escriba nombre Hola de nuevo complemento SAML hello y haga clic en hello **'Add'** botón.</span><span class="sxs-lookup"><span data-stu-id="17208-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="17208-178">Escriba los detalles de hello como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="17208-178">Enter hello details as follows:</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="17208-180">a.</span><span class="sxs-lookup"><span data-stu-id="17208-180">a.</span></span> <span data-ttu-id="17208-181">Hola **nombre** cuadro de texto, nombre de tipo hello de complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="17208-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="17208-182">b.</span><span class="sxs-lookup"><span data-stu-id="17208-182">b.</span></span> <span data-ttu-id="17208-183">Hola **dirección URL del emisor** cuadro de texto, pegue hello **Id. de entidad SAML** que copió de hello **configurar inicio de sesión** ventana de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17208-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="17208-184">c.</span><span class="sxs-lookup"><span data-stu-id="17208-184">c.</span></span> <span data-ttu-id="17208-185">Hola **configuración de metadatos del proveedor** cargar Hola archivo Metadata XML que descargó desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17208-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="17208-186">d.</span><span class="sxs-lookup"><span data-stu-id="17208-186">d.</span></span> <span data-ttu-id="17208-187">También puede elegir tooenable SAML aprovisionamiento justo a tiempo habilitando hello **'Creación automática de nuevos usuarios'** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="17208-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="17208-188">Si un usuario no existe en Velpic y esta marca no está habilitada, se producirá un error de inicio de sesión de Hola de Azure.</span><span class="sxs-lookup"><span data-stu-id="17208-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="17208-189">Si marca Hola estará habilitado Hola usuario automáticamente aprovisionar en Velpic en tiempo de Hola de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="17208-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="17208-190">e.</span><span class="sxs-lookup"><span data-stu-id="17208-190">e.</span></span> <span data-ttu-id="17208-191">Hola copia **en dirección URL de inicio de sesión único** de cuadro de texto de Hola y lo pega en Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17208-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="17208-192">f.</span><span class="sxs-lookup"><span data-stu-id="17208-192">f.</span></span> <span data-ttu-id="17208-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="17208-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17208-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17208-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="17208-195">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="17208-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="17208-197">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17208-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17208-198">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="17208-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17208-200">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="17208-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17208-202">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17208-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17208-204">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="17208-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17208-206">a.</span><span class="sxs-lookup"><span data-stu-id="17208-206">a.</span></span> <span data-ttu-id="17208-207">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17208-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17208-208">b.</span><span class="sxs-lookup"><span data-stu-id="17208-208">b.</span></span> <span data-ttu-id="17208-209">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17208-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17208-210">c.</span><span class="sxs-lookup"><span data-stu-id="17208-210">c.</span></span> <span data-ttu-id="17208-211">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="17208-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17208-212">d.</span><span class="sxs-lookup"><span data-stu-id="17208-212">d.</span></span> <span data-ttu-id="17208-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="17208-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="17208-214">Creación de un usuario de prueba de Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="17208-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="17208-215">Normalmente este paso no es necesario que sea compatible con aplicación hello justo a tiempo el aprovisionamiento de usuarios.</span><span class="sxs-lookup"><span data-stu-id="17208-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="17208-216">Si no está habilitado el aprovisionamiento automático de usuarios de hello creación manual del usuario puede realizarse tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="17208-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="17208-217">Inicie sesión como administrador en su sitio de la compañía de Velpic SAML y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="17208-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="17208-218">Haga clic en la ficha administrar y vaya sección tooUsers, a continuación, haga clic en nuevo botón tooadd usuarios.</span><span class="sxs-lookup"><span data-stu-id="17208-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![agregar usuario](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="17208-220">En hello **"Crear nuevo usuario"** cuadro de diálogo, siga los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="17208-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="17208-222">a.</span><span class="sxs-lookup"><span data-stu-id="17208-222">a.</span></span> <span data-ttu-id="17208-223">Hola **nombre** cuadro de texto Nombre tipo hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17208-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="17208-224">b.</span><span class="sxs-lookup"><span data-stu-id="17208-224">b.</span></span> <span data-ttu-id="17208-225">Hola **Last Name** cuadro de texto, escriba Hola apellidos de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17208-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="17208-226">c.</span><span class="sxs-lookup"><span data-stu-id="17208-226">c.</span></span> <span data-ttu-id="17208-227">Hola **nombre de usuario** cuadro de texto, escriba el nombre de usuario de Hola de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17208-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="17208-228">d.</span><span class="sxs-lookup"><span data-stu-id="17208-228">d.</span></span> <span data-ttu-id="17208-229">Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17208-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="17208-230">e.</span><span class="sxs-lookup"><span data-stu-id="17208-230">e.</span></span> <span data-ttu-id="17208-231">Resto de información de hello es opcional, que puede rellenar si es necesario.</span><span class="sxs-lookup"><span data-stu-id="17208-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="17208-232">f.</span><span class="sxs-lookup"><span data-stu-id="17208-232">f.</span></span> <span data-ttu-id="17208-233">Haga clic en **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="17208-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17208-234">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17208-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17208-235">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooVelpic acceso SAML.</span><span class="sxs-lookup"><span data-stu-id="17208-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="17208-237">**tooassign Britta Simon tooVelpic SAML, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="17208-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="17208-238">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17208-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="17208-240">En la lista de aplicaciones de hello, seleccione **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="17208-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="17208-242">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17208-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="17208-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="17208-244">Click **Add** button.</span></span> <span data-ttu-id="17208-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17208-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="17208-247">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="17208-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17208-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17208-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17208-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17208-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17208-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="17208-250">Testing single sign-on</span></span>

<span data-ttu-id="17208-251">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="17208-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="17208-252">Al hacer clic en hello Velpic SAML disponer en mosaico en hello Panel de acceso, deberá obtener la página de inicio de sesión de aplicación Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="17208-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="17208-253">Debería ver Hola **'Iniciar sesión con Azure AD'** botón de inicio de sesión de hello en la página.</span><span class="sxs-lookup"><span data-stu-id="17208-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="17208-255">Haga clic en hello **'Iniciar sesión con Azure AD'** toolog de botón en tooVelpic con su cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17208-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="17208-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="17208-256">Additional resources</span></span>

* [<span data-ttu-id="17208-257">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17208-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17208-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17208-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

