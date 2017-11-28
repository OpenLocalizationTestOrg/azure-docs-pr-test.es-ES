---
title: "Tutorial: Integración de Azure Active Directory con Proofpoint on Demand | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Proofpoint a petición."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="ed113-103">Tutorial: Integración de Azure Active Directory con Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="ed113-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="ed113-104">En este tutorial, aprenderá cómo toointegrate Proofpoint a petición con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed113-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed113-105">Integración Proofpoint a petición con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ed113-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ed113-106">Puede controlar en Azure AD que tenga acceso tooProofpoint a petición</span><span class="sxs-lookup"><span data-stu-id="ed113-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="ed113-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooProofpoint a petición (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed113-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed113-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ed113-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ed113-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed113-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed113-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ed113-110">Prerequisites</span></span>

<span data-ttu-id="ed113-111">integración de Azure AD tooconfigure con Proofpoint a petición, es necesario Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ed113-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="ed113-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed113-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed113-113">Una suscripción habilitada para el inicio de sesión único en Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="ed113-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed113-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ed113-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed113-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ed113-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed113-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ed113-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed113-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed113-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed113-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ed113-118">Scenario description</span></span>
<span data-ttu-id="ed113-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ed113-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed113-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ed113-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed113-121">Agregar Proofpoint a petición desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ed113-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="ed113-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed113-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="ed113-123">Agregar Proofpoint a petición desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ed113-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="ed113-124">integración de hello tooconfigure de Proofpoint a petición en Azure AD, deberá tooadd Proofpoint a petición de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ed113-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ed113-125">**tooadd Proofpoint a petición desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ed113-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed113-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ed113-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed113-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ed113-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ed113-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ed113-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ed113-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ed113-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ed113-133">En el cuadro de búsqueda de hello, escriba **Proofpoint a petición**.</span><span class="sxs-lookup"><span data-stu-id="ed113-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="ed113-135">En el panel de resultados de hello, seleccione **Proofpoint a petición**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ed113-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed113-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed113-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed113-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Proofpoint on Demand con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ed113-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ed113-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Proofpoint a petición es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed113-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="ed113-140">En otras palabras, una relación entre un usuario de Azure AD y el usuario relacionado de hello en Proofpoint a petición de vínculo debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ed113-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="ed113-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Proofpoint a petición.</span><span class="sxs-lookup"><span data-stu-id="ed113-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="ed113-142">prueba Azure AD y tooconfigure inicio de sesión único con Proofpoint a petición, es necesario hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ed113-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ed113-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ed113-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ed113-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed113-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed113-145">**[Crear un Proofpoint en usuario de prueba de petición](#creating-a-proofpoint-on-demand-test-user)**  -toohave un equivalente de Britta Simon en Proofpoint a petición que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="ed113-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed113-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ed113-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed113-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ed113-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed113-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed113-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed113-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su Proofpoint en aplicación de la demanda.</span><span class="sxs-lookup"><span data-stu-id="ed113-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="ed113-150">**inicio de sesión único en Azure AD tooconfigure con Proofpoint a petición, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ed113-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed113-151">En el portal de Azure, en Hola Hola **Proofpoint a petición** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ed113-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ed113-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ed113-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="ed113-155">En hello **Proofpoint en los dominios de petición y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ed113-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="ed113-157">Hola a.In **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="ed113-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="ed113-158">b.</span><span class="sxs-lookup"><span data-stu-id="ed113-158">b.</span></span> <span data-ttu-id="ed113-159">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="ed113-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="ed113-160">c.</span><span class="sxs-lookup"><span data-stu-id="ed113-160">c.</span></span>  <span data-ttu-id="ed113-161">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="ed113-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ed113-162">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="ed113-162">These values are not hello real.</span></span> <span data-ttu-id="ed113-163">Actualizar estos valores con hello real identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ed113-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="ed113-164">Póngase en contacto con [Proofpoint en el equipo de soporte técnico de cliente de petición](https://www.proofpoint.com/us/support-services) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="ed113-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="ed113-165">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ed113-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="ed113-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ed113-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ed113-169">En hello **Proofpoint en configuración de la petición** sección, haga clic en **configurar Proofpoint a petición** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="ed113-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ed113-170">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="ed113-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="ed113-172">inicio de sesión único en tooconfigure en **Proofpoint a petición** lado, necesita hello toosend descargado **Certificate(Base64)**,**Id. de entidad SAML**, y **SAML Solo la dirección URL del servicio Inicio de sesión** demasiado[Proofpoint en el equipo de soporte técnico de cliente de petición](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="ed113-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="ed113-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="ed113-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ed113-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="ed113-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ed113-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed113-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed113-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed113-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed113-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ed113-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ed113-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ed113-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed113-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ed113-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed113-182">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="ed113-182">These values are not hello real.</span></span> <span data-ttu-id="ed113-183">Actualizar estos valores con hello real</span><span class="sxs-lookup"><span data-stu-id="ed113-183">Update these values with hello actual</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed113-185">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed113-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed113-187">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ed113-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed113-189">a.</span><span class="sxs-lookup"><span data-stu-id="ed113-189">a.</span></span> <span data-ttu-id="ed113-190">Hola **nombre** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ed113-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="ed113-191">b.</span><span class="sxs-lookup"><span data-stu-id="ed113-191">b.</span></span> <span data-ttu-id="ed113-192">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed113-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="ed113-193">c.</span><span class="sxs-lookup"><span data-stu-id="ed113-193">c.</span></span> <span data-ttu-id="ed113-194">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ed113-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ed113-195">d.</span><span class="sxs-lookup"><span data-stu-id="ed113-195">d.</span></span> <span data-ttu-id="ed113-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ed113-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="ed113-197">Creación de un usuario de prueba de Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="ed113-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="ed113-198">En esta sección, creará un usuario llamado Britta Simon en Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ed113-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="ed113-199">Trabajar con [Proofpoint en el equipo de soporte técnico de cliente de petición](https://www.proofpoint.com/us/support-services) usuarios tooadd Hola Proofpoint en plataforma de petición.</span><span class="sxs-lookup"><span data-stu-id="ed113-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ed113-200">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed113-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ed113-201">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooProofpoint a petición.</span><span class="sxs-lookup"><span data-stu-id="ed113-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ed113-203">**tooassign Britta Simon tooProofpoint bajo demanda, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ed113-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed113-204">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ed113-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ed113-206">En la lista de aplicaciones de hello, seleccione **Proofpoint a petición**.</span><span class="sxs-lookup"><span data-stu-id="ed113-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="ed113-208">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ed113-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ed113-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ed113-210">Click **Add** button.</span></span> <span data-ttu-id="ed113-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ed113-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ed113-213">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed113-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ed113-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ed113-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed113-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ed113-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed113-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ed113-216">Testing single sign-on</span></span>

<span data-ttu-id="ed113-217">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ed113-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ed113-218">Al hacer clic en hello **Proofpoint a petición** icono Hola Panel de acceso, debe firmarse automáticamente en tooyour Proofpoint en aplicación de la demanda.</span><span class="sxs-lookup"><span data-stu-id="ed113-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="ed113-219">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ed113-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="ed113-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ed113-220">Additional resources</span></span>

* [<span data-ttu-id="ed113-221">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed113-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed113-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed113-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

