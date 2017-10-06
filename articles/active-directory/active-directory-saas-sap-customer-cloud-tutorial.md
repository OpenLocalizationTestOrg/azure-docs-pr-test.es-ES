---
title: "Tutorial: Integración de Azure Active Directory con SAP Cloud for Customer | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la nube de SAP para el cliente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="8543e-103">Tutorial: Integración de Azure Active Directory con SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="8543e-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="8543e-104">En este tutorial, aprenderá cómo toointegrate SAP en la nube para el cliente con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8543e-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8543e-105">Integración de SAP en la nube para el cliente con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8543e-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8543e-106">Puede controlar en Azure AD que tiene acceso tooSAP en la nube para cliente</span><span class="sxs-lookup"><span data-stu-id="8543e-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="8543e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAP en la nube de cliente (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8543e-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8543e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8543e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8543e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8543e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8543e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8543e-110">Prerequisites</span></span>

<span data-ttu-id="8543e-111">tooconfigure integración de Azure AD con SAP en la nube para el cliente, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8543e-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="8543e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8543e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8543e-113">Una suscripción a SAP Cloud for Customer con inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="8543e-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8543e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8543e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8543e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8543e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8543e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8543e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8543e-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8543e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8543e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8543e-118">Scenario description</span></span>
<span data-ttu-id="8543e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8543e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8543e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8543e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8543e-121">Agregar en la nube SAP de cliente desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8543e-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="8543e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8543e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="8543e-123">Agregar en la nube SAP de cliente desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8543e-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="8543e-124">integración de hello tooconfigure de SAP en la nube para el cliente en Azure AD, necesitará tooadd en la nube SAP para cliente de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8543e-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8543e-125">**tooadd en la nube SAP para cliente de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8543e-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8543e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8543e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8543e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8543e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8543e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8543e-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8543e-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8543e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8543e-133">En el cuadro de búsqueda de hello, escriba **en la nube SAP para cliente**.</span><span class="sxs-lookup"><span data-stu-id="8543e-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="8543e-135">En el panel de resultados de hello, seleccione **en la nube SAP para cliente**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8543e-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8543e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8543e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8543e-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con SAP Cloud for Customer con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8543e-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8543e-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en la nube de SAP para el cliente es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8543e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="8543e-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en la nube de SAP para el cliente debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8543e-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="8543e-141">En la nube de SAP para el cliente, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8543e-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8543e-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SAP en la nube para el cliente, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8543e-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8543e-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8543e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8543e-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8543e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8543e-145">**[Crear una nube de SAP de usuario de cliente de prueba](#creating-a-sap-cloud-for-customer-test-user)**  -toohave un equivalente de Britta Simon en nube de SAP para cliente que es la representación en forma de toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8543e-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8543e-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8543e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8543e-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8543e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8543e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8543e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8543e-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la nube de SAP para la aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="8543e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="8543e-150">**tooconfigure inicio de sesión único en Azure AD con SAP en la nube para el cliente, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8543e-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="8543e-151">En el portal de Azure, en Hola Hola **en la nube SAP para cliente** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8543e-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8543e-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8543e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="8543e-155">En hello **SAP en la nube para el dominio del cliente y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8543e-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="8543e-157">a.</span><span class="sxs-lookup"><span data-stu-id="8543e-157">a.</span></span> <span data-ttu-id="8543e-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="8543e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="8543e-159">b.</span><span class="sxs-lookup"><span data-stu-id="8543e-159">b.</span></span> <span data-ttu-id="8543e-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="8543e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8543e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="8543e-161">These values are not real.</span></span> <span data-ttu-id="8543e-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="8543e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8543e-163">Póngase en contacto con [SAP en la nube para el equipo de soporte técnico al cliente cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="8543e-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="8543e-164">En hello **atributos de usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8543e-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="8543e-166">a.</span><span class="sxs-lookup"><span data-stu-id="8543e-166">a.</span></span> <span data-ttu-id="8543e-167">En **identificador de usuario** lista, seleccione hello **ExtractMailPrefix()** (función).</span><span class="sxs-lookup"><span data-stu-id="8543e-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="8543e-168">b.</span><span class="sxs-lookup"><span data-stu-id="8543e-168">b.</span></span> <span data-ttu-id="8543e-169">De hello **correo** lista, atributo de usuario de hello seleccione desea toouse para su implementación.</span><span class="sxs-lookup"><span data-stu-id="8543e-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="8543e-170">Por ejemplo, si desea toouse Hola EmployeeID como identificador de usuario único y lo ha almacenado el valor del atributo de Hola Hola ExtensionAttribute2, a continuación, seleccione user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="8543e-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="8543e-171">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8543e-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="8543e-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8543e-173">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8543e-175">En hello **en la nube para la configuración de cliente de SAP** sección, haga clic en **configurar la nube de SAP para cliente** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="8543e-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8543e-176">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8543e-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="8543e-178">tooget SSO configurado, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8543e-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="8543e-179">a.</span><span class="sxs-lookup"><span data-stu-id="8543e-179">a.</span></span> <span data-ttu-id="8543e-180">Inicie sesión en el portal de SAP Cloud for Customer con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="8543e-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="8543e-181">b.</span><span class="sxs-lookup"><span data-stu-id="8543e-181">b.</span></span> <span data-ttu-id="8543e-182">Navegue toohello **aplicación y tareas comunes de administración de usuario** y haga clic en hello **proveedor de identidades** ficha.</span><span class="sxs-lookup"><span data-stu-id="8543e-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="8543e-183">c.</span><span class="sxs-lookup"><span data-stu-id="8543e-183">c.</span></span> <span data-ttu-id="8543e-184">Haga clic en **nuevo proveedor de identidades** Hola seleccione metadatos del archivo XML y ha descargado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8543e-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="8543e-185">Mediante la importación de metadatos de hello, sistema de Hola carga automáticamente el certificado de firma necesaria de Hola y el certificado de cifrado.</span><span class="sxs-lookup"><span data-stu-id="8543e-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="8543e-187">d.</span><span class="sxs-lookup"><span data-stu-id="8543e-187">d.</span></span> <span data-ttu-id="8543e-188">Azure Active Directory requiere Hola elemento dirección URL del servicio de consumidor de aserción en la solicitud SAML de hello, así que seleccione hello **incluir dirección URL del servicio de consumidor de aserción** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="8543e-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="8543e-189">e.</span><span class="sxs-lookup"><span data-stu-id="8543e-189">e.</span></span> <span data-ttu-id="8543e-190">Haga clic en **Activate Single Sign-On**(Activar inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="8543e-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="8543e-191">f.</span><span class="sxs-lookup"><span data-stu-id="8543e-191">f.</span></span> <span data-ttu-id="8543e-192">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="8543e-192">Save your changes.</span></span>
   
    <span data-ttu-id="8543e-193">g.</span><span class="sxs-lookup"><span data-stu-id="8543e-193">g.</span></span> <span data-ttu-id="8543e-194">Haga clic en hello **mi sistema** ficha.</span><span class="sxs-lookup"><span data-stu-id="8543e-194">Click hello **My System** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="8543e-196">h.</span><span class="sxs-lookup"><span data-stu-id="8543e-196">h.</span></span> <span data-ttu-id="8543e-197">En el cuadro de texto **Azure AD Sign On URL** (Dirección URL de inicio de sesión de Azure AD), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8543e-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="8543e-199">i.</span><span class="sxs-lookup"><span data-stu-id="8543e-199">i.</span></span> <span data-ttu-id="8543e-200">Especifique si empleado Hola manualmente puede elegir entre iniciar sesión con el Id. de usuario y una contraseña o SSO seleccionando hello **selección de proveedor de identidad Manual**.</span><span class="sxs-lookup"><span data-stu-id="8543e-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="8543e-201">j.</span><span class="sxs-lookup"><span data-stu-id="8543e-201">j.</span></span> <span data-ttu-id="8543e-202">Hola **dirección URL SSO** sección, especificar dirección URL de Hola que debe usarse en su toosign empleados en toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="8543e-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="8543e-203">Hola **tooEmployee envía la dirección URL** lista, puede elegir entre Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="8543e-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="8543e-204">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="8543e-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="8543e-205">sistema de Hello envía a empleado de toohello Hola solo dirección URL de la normal del sistema.</span><span class="sxs-lookup"><span data-stu-id="8543e-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="8543e-206">empleado de Hola no se puede iniciar sesión con SSO y debe utilizar la contraseña o certificado en su lugar.</span><span class="sxs-lookup"><span data-stu-id="8543e-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="8543e-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="8543e-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="8543e-208">sistema de Hello envía a solo empleado de toohello de hello dirección URL SSO.</span><span class="sxs-lookup"><span data-stu-id="8543e-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="8543e-209">empleado de Hello puede iniciar sesión con SSO.</span><span class="sxs-lookup"><span data-stu-id="8543e-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="8543e-210">Solicitud de autenticación se redirige a través de hello IdP.</span><span class="sxs-lookup"><span data-stu-id="8543e-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="8543e-211">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="8543e-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="8543e-212">Si SSO no está activo, el sistema de hello envía a empleado de toohello de dirección URL de hello normal del sistema.</span><span class="sxs-lookup"><span data-stu-id="8543e-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="8543e-213">Si SSO está activo, el sistema de Hola comprueba si empleado hello tiene una contraseña.</span><span class="sxs-lookup"><span data-stu-id="8543e-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="8543e-214">Si hay una contraseña, dirección URL de SSO y dirección URL de SSO no se envían a toohello empleado.</span><span class="sxs-lookup"><span data-stu-id="8543e-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="8543e-215">Sin embargo, si Hola empleado no tiene ninguna contraseña, sólo Hola dirección URL de SSO se envía a toohello empleado.</span><span class="sxs-lookup"><span data-stu-id="8543e-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="8543e-216">k.</span><span class="sxs-lookup"><span data-stu-id="8543e-216">k.</span></span> <span data-ttu-id="8543e-217">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="8543e-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="8543e-218">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8543e-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8543e-219">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8543e-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8543e-220">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8543e-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8543e-221">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8543e-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="8543e-222">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8543e-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8543e-224">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8543e-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8543e-225">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8543e-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8543e-227">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8543e-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8543e-229">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8543e-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8543e-231">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8543e-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8543e-233">a.</span><span class="sxs-lookup"><span data-stu-id="8543e-233">a.</span></span> <span data-ttu-id="8543e-234">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8543e-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8543e-235">b.</span><span class="sxs-lookup"><span data-stu-id="8543e-235">b.</span></span> <span data-ttu-id="8543e-236">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8543e-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8543e-237">c.</span><span class="sxs-lookup"><span data-stu-id="8543e-237">c.</span></span> <span data-ttu-id="8543e-238">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8543e-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8543e-239">d.</span><span class="sxs-lookup"><span data-stu-id="8543e-239">d.</span></span> <span data-ttu-id="8543e-240">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8543e-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="8543e-241">Creación de un usuario de prueba de SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="8543e-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="8543e-242">En esta sección, creará un usuario llamado Britta Simon en SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="8543e-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="8543e-243">Trabaje con [SAP en la nube para el equipo de soporte técnico al cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) a los usuarios de tooadd Hola Hola SAP en la nube para la plataforma de cliente.</span><span class="sxs-lookup"><span data-stu-id="8543e-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="8543e-244">Asegúrese de que NameID valor debe coincidir con el campo de nombre de usuario de Hola Hola SAP en la nube para la plataforma de cliente.</span><span class="sxs-lookup"><span data-stu-id="8543e-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8543e-245">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8543e-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8543e-246">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAP en la nube para el cliente.</span><span class="sxs-lookup"><span data-stu-id="8543e-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8543e-248">**tooassign Britta Simon tooSAP en la nube para el cliente, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8543e-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="8543e-249">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8543e-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8543e-251">En la lista de aplicaciones de hello, seleccione **en la nube SAP para cliente**.</span><span class="sxs-lookup"><span data-stu-id="8543e-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="8543e-253">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8543e-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8543e-255">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8543e-255">Click **Add** button.</span></span> <span data-ttu-id="8543e-256">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8543e-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8543e-258">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8543e-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8543e-259">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8543e-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8543e-260">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8543e-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8543e-261">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8543e-261">Testing single sign-on</span></span>

<span data-ttu-id="8543e-262">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8543e-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8543e-263">Al hacer clic en hello en la nube SAP de icono del cliente en el Panel de acceso de hello, obtendrá automáticamente ha iniciado sesión en la nube SAP tooyour para la aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="8543e-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="8543e-264">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8543e-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8543e-265">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8543e-265">Additional resources</span></span>

* [<span data-ttu-id="8543e-266">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8543e-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8543e-267">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8543e-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

