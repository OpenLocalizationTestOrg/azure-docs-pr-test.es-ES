---
title: "Tutorial: Integración de Azure Active Directory con SAP Business ByDesign | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="80272-103">Tutorial: Integración de Azure Active Directory con SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="80272-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="80272-104">En este tutorial, aprenderá cómo toointegrate SAP Business ByDesign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80272-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80272-105">Integración de SAP Business ByDesign con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="80272-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80272-106">Puede controlar en Azure AD que tenga acceso tooSAP ByDesign de negocios.</span><span class="sxs-lookup"><span data-stu-id="80272-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="80272-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAP ByDesign de negocios (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80272-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="80272-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="80272-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="80272-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80272-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80272-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="80272-110">Prerequisites</span></span>

<span data-ttu-id="80272-111">integración de Azure AD con SAP Business ByDesign tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="80272-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="80272-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80272-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80272-113">Una suscripción habilitada para el inicio de sesión único en SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="80272-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80272-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="80272-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80272-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="80272-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80272-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="80272-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80272-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80272-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80272-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="80272-118">Scenario description</span></span>
<span data-ttu-id="80272-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="80272-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80272-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="80272-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80272-121">Adición de SAP Business ByDesign de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="80272-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="80272-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80272-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="80272-123">Adición de SAP Business ByDesign de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="80272-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="80272-124">integración de hello tooconfigure de ByDesign de negocios de SAP en Azure AD, deberá tooadd SAP Business ByDesign de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="80272-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80272-125">**tooadd ByDesign de negocios de SAP desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80272-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80272-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="80272-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="80272-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="80272-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80272-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80272-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="80272-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80272-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="80272-133">En el cuadro de búsqueda de hello, escriba **SAP Business ByDesign**, seleccione **SAP Business ByDesign** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="80272-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de SAP Business ByDesign Hola](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="80272-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="80272-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="80272-136">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con SAP Business ByDesign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="80272-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="80272-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SAP Business ByDesign es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80272-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="80272-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SAP Business ByDesign debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="80272-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="80272-139">En SAP Business ByDesign, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="80272-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="80272-140">tooconfigure y prueba de inicio de sesión único en Azure AD con SAP Business ByDesign, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="80272-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80272-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="80272-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80272-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80272-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80272-143">**[Crear un usuario de prueba de SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave un equivalente de Britta Simon en SAP Business ByDesign que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="80272-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80272-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="80272-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80272-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="80272-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="80272-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80272-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="80272-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="80272-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="80272-148">**tooconfigure inicio de sesión único en Azure AD con SAP Business ByDesign, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80272-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="80272-149">En el portal de Azure, en Hola Hola **SAP Business ByDesign** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="80272-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="80272-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="80272-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="80272-153">En hello **SAP Business ByDesign dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="80272-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="80272-155">a.</span><span class="sxs-lookup"><span data-stu-id="80272-155">a.</span></span> <span data-ttu-id="80272-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="80272-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="80272-157">b.</span><span class="sxs-lookup"><span data-stu-id="80272-157">b.</span></span> <span data-ttu-id="80272-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="80272-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="80272-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="80272-159">These values are not real.</span></span> <span data-ttu-id="80272-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="80272-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="80272-161">Póngase en contacto con [equipo de soporte técnico de SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="80272-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="80272-162">En hello **atributos de usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="80272-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Sección Atributos de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="80272-164">a.</span><span class="sxs-lookup"><span data-stu-id="80272-164">a.</span></span> <span data-ttu-id="80272-165">En **identificador de usuario** lista, seleccione hello **ExtractMailPrefix()** (función).</span><span class="sxs-lookup"><span data-stu-id="80272-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="80272-166">b.</span><span class="sxs-lookup"><span data-stu-id="80272-166">b.</span></span> <span data-ttu-id="80272-167">De hello **correo** lista, atributo de usuario de hello seleccione desea toouse para su implementación.</span><span class="sxs-lookup"><span data-stu-id="80272-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="80272-168">Por ejemplo, si desea toouse Hola EmployeeID como identificador de usuario único y lo ha almacenado el valor del atributo de Hola Hola ExtensionAttribute2, a continuación, seleccione user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="80272-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="80272-169">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="80272-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="80272-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="80272-171">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="80272-173">En hello **configuración de SAP Business ByDesign** sección, haga clic en **configurar SAP Business ByDesign** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="80272-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="80272-174">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="80272-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="80272-176">tooget SSO configurado para la aplicación, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="80272-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="80272-177">a.</span><span class="sxs-lookup"><span data-stu-id="80272-177">a.</span></span> <span data-ttu-id="80272-178">Inicie sesión en el portal de SAP Business ByDesign tooyour con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="80272-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="80272-179">b.</span><span class="sxs-lookup"><span data-stu-id="80272-179">b.</span></span> <span data-ttu-id="80272-180">Navegue demasiado**aplicación y tareas comunes de administración de usuario** y haga clic en hello **proveedor de identidades** ficha.</span><span class="sxs-lookup"><span data-stu-id="80272-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="80272-181">c.</span><span class="sxs-lookup"><span data-stu-id="80272-181">c.</span></span> <span data-ttu-id="80272-182">Haga clic en **nuevo proveedor de identidades** y archivo XML de metadatos de hello select que ha descargado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="80272-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="80272-183">Mediante la importación de metadatos de hello, sistema de Hola carga automáticamente el certificado de firma necesaria de Hola y el certificado de cifrado.</span><span class="sxs-lookup"><span data-stu-id="80272-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="80272-185">d.</span><span class="sxs-lookup"><span data-stu-id="80272-185">d.</span></span> <span data-ttu-id="80272-186">Hola tooinclude **dirección URL del servicio de consumidor de aserción** en la solicitud SAML de hello, seleccione **incluir dirección URL del servicio de consumidor de aserción**.</span><span class="sxs-lookup"><span data-stu-id="80272-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="80272-187">e.</span><span class="sxs-lookup"><span data-stu-id="80272-187">e.</span></span> <span data-ttu-id="80272-188">Haga clic en **Activate Single Sign-On**(Activar inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="80272-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="80272-189">f.</span><span class="sxs-lookup"><span data-stu-id="80272-189">f.</span></span> <span data-ttu-id="80272-190">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="80272-190">Save your changes.</span></span>
   
    <span data-ttu-id="80272-191">g.</span><span class="sxs-lookup"><span data-stu-id="80272-191">g.</span></span> <span data-ttu-id="80272-192">Haga clic en hello **mi sistema** ficha.</span><span class="sxs-lookup"><span data-stu-id="80272-192">Click hello **My System** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="80272-194">h.</span><span class="sxs-lookup"><span data-stu-id="80272-194">h.</span></span> <span data-ttu-id="80272-195">Pegar **SAML Single Sign-On dirección URL del servicio**, que lo ha copiado desde el portal de Azure de hello en hello **inicio de sesión de Azure AD en la dirección URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="80272-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="80272-197">i.</span><span class="sxs-lookup"><span data-stu-id="80272-197">i.</span></span> <span data-ttu-id="80272-198">Especifique si el empleado Hola manualmente puede elegir entre iniciar sesión con el Id. de usuario y una contraseña o SSO seleccionando **selección de proveedor de identidad Manual**.</span><span class="sxs-lookup"><span data-stu-id="80272-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="80272-199">j.</span><span class="sxs-lookup"><span data-stu-id="80272-199">j.</span></span> <span data-ttu-id="80272-200">Hola **dirección URL SSO** sección, especificar dirección URL de Hola que debe utilizar Hola empleado toologon toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="80272-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="80272-201">En lista de desplegable de tooEmployee URL enviados hello, puede elegir entre Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="80272-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="80272-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="80272-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="80272-203">sistema de Hello envía a empleado de toohello Hola solo dirección URL de la normal del sistema.</span><span class="sxs-lookup"><span data-stu-id="80272-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="80272-204">empleado de Hola no se puede iniciar sesión con SSO y debe utilizar la contraseña o certificado en su lugar.</span><span class="sxs-lookup"><span data-stu-id="80272-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="80272-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="80272-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="80272-206">sistema de Hello envía a solo empleado de toohello de hello dirección URL SSO.</span><span class="sxs-lookup"><span data-stu-id="80272-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="80272-207">empleado de Hello puede iniciar sesión con SSO.</span><span class="sxs-lookup"><span data-stu-id="80272-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="80272-208">Solicitud de autenticación se redirige a través de hello IdP.</span><span class="sxs-lookup"><span data-stu-id="80272-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="80272-209">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="80272-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="80272-210">Si SSO no está activo, el sistema de hello envía a empleado de toohello de dirección URL de hello normal del sistema.</span><span class="sxs-lookup"><span data-stu-id="80272-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="80272-211">Si SSO está activo, el sistema de Hola comprueba si empleado hello tiene una contraseña.</span><span class="sxs-lookup"><span data-stu-id="80272-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="80272-212">Si hay una contraseña, dirección URL de SSO y dirección URL de SSO no se envían a toohello empleado.</span><span class="sxs-lookup"><span data-stu-id="80272-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="80272-213">Sin embargo, si Hola empleado no tiene ninguna contraseña, sólo Hola dirección URL de SSO se envía a toohello empleado.</span><span class="sxs-lookup"><span data-stu-id="80272-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="80272-214">k.</span><span class="sxs-lookup"><span data-stu-id="80272-214">k.</span></span> <span data-ttu-id="80272-215">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="80272-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="80272-216">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="80272-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80272-217">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="80272-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80272-218">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80272-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="80272-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80272-219">Create an Azure AD test user</span></span>

<span data-ttu-id="80272-220">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="80272-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="80272-222">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80272-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80272-223">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="80272-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="80272-225">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="80272-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="80272-227">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80272-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="80272-229">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="80272-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="80272-231">a.</span><span class="sxs-lookup"><span data-stu-id="80272-231">a.</span></span> <span data-ttu-id="80272-232">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80272-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80272-233">b.</span><span class="sxs-lookup"><span data-stu-id="80272-233">b.</span></span> <span data-ttu-id="80272-234">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80272-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="80272-235">c.</span><span class="sxs-lookup"><span data-stu-id="80272-235">c.</span></span> <span data-ttu-id="80272-236">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="80272-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="80272-237">d.</span><span class="sxs-lookup"><span data-stu-id="80272-237">d.</span></span> <span data-ttu-id="80272-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="80272-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="80272-239">Creación de un usuario de prueba de SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="80272-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="80272-240">En esta sección, creará un usuario llamado Britta Simon en SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="80272-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="80272-241">Trabaje con [equipo de soporte técnico de SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) a los usuarios de tooadd hello en la plataforma de SAP Business ByDesign Hola.</span><span class="sxs-lookup"><span data-stu-id="80272-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="80272-242">Asegúrese de que NameID valor debe coincidir con el campo de nombre de usuario de hello en la plataforma de SAP Business ByDesign Hola.</span><span class="sxs-lookup"><span data-stu-id="80272-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="80272-243">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="80272-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="80272-244">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAP ByDesign de negocios.</span><span class="sxs-lookup"><span data-stu-id="80272-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="80272-246">**tooassign Britta Simon tooSAP ByDesign de negocios, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80272-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="80272-247">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80272-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="80272-249">En la lista de aplicaciones de hello, seleccione **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="80272-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![vínculo de SAP Business ByDesign Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="80272-251">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80272-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="80272-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="80272-253">Click **Add** button.</span></span> <span data-ttu-id="80272-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80272-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="80272-256">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="80272-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80272-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80272-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80272-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80272-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="80272-259">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="80272-259">Test single sign-on</span></span>

<span data-ttu-id="80272-260">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="80272-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80272-261">Al hacer clic en icono de SAP Business ByDesign Hola Hola Panel de acceso, deberá obtener la aplicación de SAP Business ByDesign tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="80272-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80272-262">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="80272-262">Additional resources</span></span>

* [<span data-ttu-id="80272-263">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80272-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80272-264">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80272-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

