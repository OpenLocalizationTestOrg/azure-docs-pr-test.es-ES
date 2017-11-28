---
title: "Tutorial: integración de Azure Active Directory con SAP NetWeaver | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 69008734864e1e258a0c2ec872e51aa331491fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="aa47c-103">Tutorial: Integración de Azure Active Directory con SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="aa47c-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="aa47c-104">En este tutorial, aprenderá cómo toointegrate SAP NetWeaver con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa47c-104">In this tutorial, you learn how toointegrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa47c-105">Integración de SAP NetWeaver en Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="aa47c-105">Integrating SAP NetWeaver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa47c-106">Puede controlar en Azure AD que tenga acceso tooSAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="aa47c-106">You can control in Azure AD who has access tooSAP NetWeaver</span></span>
- <span data-ttu-id="aa47c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAP NetWeaver (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa47c-107">You can enable your users tooautomatically get signed-on tooSAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa47c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="aa47c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aa47c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa47c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="aa47c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aa47c-110">Prerequisites</span></span>

<span data-ttu-id="aa47c-111">tooconfigure integración de Azure AD con SAP NetWeaver, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="aa47c-111">tooconfigure Azure AD integration with SAP NetWeaver, you need hello following items:</span></span>

- <span data-ttu-id="aa47c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa47c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa47c-113">Una suscripción habilitada para el inicio de sesión único en SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="aa47c-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa47c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="aa47c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa47c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="aa47c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa47c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aa47c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa47c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa47c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa47c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="aa47c-118">Scenario description</span></span>
<span data-ttu-id="aa47c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="aa47c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa47c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="aa47c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa47c-121">Adición de SAP NetWeaver desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aa47c-121">Adding SAP NetWeaver from hello gallery</span></span>
2. <span data-ttu-id="aa47c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa47c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-hello-gallery"></a><span data-ttu-id="aa47c-123">Adición de SAP NetWeaver desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aa47c-123">Adding SAP NetWeaver from hello gallery</span></span>
<span data-ttu-id="aa47c-124">integración de hello tooconfigure de SAP NetWeaver en Azure AD, deberá tooadd SAP NetWeaver en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="aa47c-124">tooconfigure hello integration of SAP NetWeaver into Azure AD, you need tooadd SAP NetWeaver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa47c-125">**tooadd SAP NetWeaver desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa47c-125">**tooadd SAP NetWeaver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa47c-126">Hola  **[Portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="aa47c-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa47c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa47c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="aa47c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa47c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="aa47c-133">En el cuadro de búsqueda de hello, escriba **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-133">In hello search box, type **SAP NetWeaver**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="aa47c-135">En el panel de resultados de hello, seleccione **SAP NetWeaver**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aa47c-135">In hello results panel, select **SAP NetWeaver**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa47c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa47c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa47c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SAP NetWeaver utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa47c-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aa47c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SAP NetWeaver es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa47c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP NetWeaver is tooa user in Azure AD.</span></span> <span data-ttu-id="aa47c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SAP NetWeaver debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="aa47c-140">In other words, a link relationship between an Azure AD user and hello related user in SAP NetWeaver needs toobe established.</span></span>

<span data-ttu-id="aa47c-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="aa47c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="aa47c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SAP NetWeaver, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="aa47c-142">tooconfigure and test Azure AD single sign-on with SAP NetWeaver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa47c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="aa47c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa47c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa47c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa47c-145">**[Creación de un usuario de prueba de SAP NetWeaver](#creating-an-sap-netweaver-test-user)**  -toohave un equivalente de Britta Simon en SAP NetWeaver que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="aa47c-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - toohave a counterpart of Britta Simon in SAP NetWeaver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa47c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aa47c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa47c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="aa47c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa47c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa47c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa47c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="aa47c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="aa47c-150">**inicio de sesión único en Azure AD tooconfigure con SAP NetWeaver, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa47c-150">**tooconfigure Azure AD single sign-on with SAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa47c-151">En el portal de Azure, en Hola Hola **SAP NetWeaver** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-151">In hello Azure portal, on hello **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="aa47c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aa47c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="aa47c-155">En hello **SAP NetWeaver dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="aa47c-155">On hello **SAP NetWeaver Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="aa47c-157">a.</span><span class="sxs-lookup"><span data-stu-id="aa47c-157">a.</span></span> <span data-ttu-id="aa47c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="aa47c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="aa47c-159">b.</span><span class="sxs-lookup"><span data-stu-id="aa47c-159">b.</span></span> <span data-ttu-id="aa47c-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="aa47c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="aa47c-161">c.</span><span class="sxs-lookup"><span data-stu-id="aa47c-161">c.</span></span> <span data-ttu-id="aa47c-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="aa47c-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="aa47c-163">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="aa47c-163">These values are not hello real.</span></span> <span data-ttu-id="aa47c-164">Actualizar estos valores con hello real identificador y la dirección URL de respuesta y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="aa47c-164">Update these values with hello actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="aa47c-165">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="aa47c-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="aa47c-166">Póngase en contacto con [equipo de soporte técnico de SAP NetWeaver cliente](https://www.sap.com/support.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="aa47c-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) tooget these values.</span></span> 

4. <span data-ttu-id="aa47c-167">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="aa47c-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="aa47c-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="aa47c-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="aa47c-171">En hello **configuración de SAP NetWeaver** sección, haga clic en **configurar SAP NetWeaver** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="aa47c-171">On hello **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aa47c-172">Hola copia **Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="aa47c-172">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="aa47c-174">tooconfigure inicio de sesión único en **SAP NetWeaver** lado, necesita hello toosend descargado **Metadata XML** y **Id. de entidad SAML** demasiado[soporte técnico de SAP NetWeaver ](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="aa47c-174">tooconfigure single sign-on on **SAP NetWeaver** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="aa47c-175">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="aa47c-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aa47c-176">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="aa47c-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aa47c-177">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa47c-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa47c-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa47c-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa47c-179">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="aa47c-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="aa47c-181">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa47c-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa47c-182">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="aa47c-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa47c-184">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa47c-186">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa47c-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa47c-188">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="aa47c-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa47c-190">a.</span><span class="sxs-lookup"><span data-stu-id="aa47c-190">a.</span></span> <span data-ttu-id="aa47c-191">Hola **nombre** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-191">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="aa47c-192">b.</span><span class="sxs-lookup"><span data-stu-id="aa47c-192">b.</span></span> <span data-ttu-id="aa47c-193">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa47c-193">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="aa47c-194">c.</span><span class="sxs-lookup"><span data-stu-id="aa47c-194">c.</span></span> <span data-ttu-id="aa47c-195">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aa47c-196">d.</span><span class="sxs-lookup"><span data-stu-id="aa47c-196">d.</span></span> <span data-ttu-id="aa47c-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="aa47c-198">Creación de un usuario de prueba de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="aa47c-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="aa47c-199">En esta sección, creará un usuario llamado Britta Simon en SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="aa47c-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="aa47c-200">Trabajar con su [soporte técnico de SAP NetWeaver](https://www.sap.com/support.html) a los usuarios de tooadd hello en la plataforma de SAP NetWeaver Hola.</span><span class="sxs-lookup"><span data-stu-id="aa47c-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) tooadd hello users in hello SAP NetWeaver platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aa47c-201">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa47c-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aa47c-202">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="aa47c-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP NetWeaver.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="aa47c-204">**tooassign Britta Simon tooSAP NetWeaver, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa47c-204">**tooassign Britta Simon tooSAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa47c-205">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="aa47c-207">En la lista de aplicaciones de hello, seleccione **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-207">In hello applications list, select **SAP NetWeaver**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="aa47c-209">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="aa47c-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-211">Click **Add** button.</span></span> <span data-ttu-id="aa47c-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="aa47c-214">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa47c-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa47c-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa47c-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa47c-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa47c-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="aa47c-217">Testing single sign-on</span></span>

<span data-ttu-id="aa47c-218">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="aa47c-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aa47c-219">Al hacer clic en icono de SAP NetWeaver Hola Hola Panel de acceso, deberá obtener la aplicación de SAP NetWeaver tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="aa47c-219">When you click hello SAP NetWeaver tile in hello Access Panel, you should get automatically signed-on tooyour SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa47c-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="aa47c-220">Additional resources</span></span>

* [<span data-ttu-id="aa47c-221">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa47c-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa47c-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa47c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

