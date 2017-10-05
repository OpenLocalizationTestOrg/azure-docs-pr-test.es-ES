---
title: "Tutorial: Integración de Azure Active Directory con Deputy | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Deputy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="2dc9d-103">Tutorial: integración de Azure Active Directory con Deputy</span><span class="sxs-lookup"><span data-stu-id="2dc9d-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="2dc9d-104">En este tutorial, aprenderá a integrar Deputy con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2dc9d-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2dc9d-105">Integrar Deputy con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2dc9d-106">Puede controlar en Azure AD quién tiene acceso a Deputy.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="2dc9d-107">Puede permitir que los usuarios inicien sesión automáticamente en Deputy (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2dc9d-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2dc9d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2dc9d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dc9d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2dc9d-110">Prerequisites</span></span>

<span data-ttu-id="2dc9d-111">Para configurar la integración de Azure AD con Deputy, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="2dc9d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dc9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2dc9d-113">Una suscripción habilitada para el inicio de sesión único en Deputy</span><span class="sxs-lookup"><span data-stu-id="2dc9d-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2dc9d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2dc9d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2dc9d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2dc9d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2dc9d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2dc9d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2dc9d-118">Scenario description</span></span>
<span data-ttu-id="2dc9d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2dc9d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2dc9d-121">Adición de Deputy desde la galería</span><span class="sxs-lookup"><span data-stu-id="2dc9d-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="2dc9d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dc9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="2dc9d-123">Adición de Deputy desde la galería</span><span class="sxs-lookup"><span data-stu-id="2dc9d-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="2dc9d-124">Para configurar la integración de Deputy en Azure AD, es preciso agregar Deputy desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2dc9d-125">**Para agregar Deputy desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2dc9d-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2dc9d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2dc9d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2dc9d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2dc9d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2dc9d-133">En el cuadro de búsqueda, escriba **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-133">In the search box, type **Deputy**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="2dc9d-135">En el panel de resultados, seleccione **Deputy** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2dc9d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dc9d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2dc9d-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Deputy con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2dc9d-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2dc9d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Deputy para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="2dc9d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Deputy.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="2dc9d-141">Para establecer la relación de vínculo, en Deputy, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2dc9d-142">Para configurar y probar el inicio de sesión único de Azure AD con Deputy, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2dc9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2dc9d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2dc9d-145">**[Creación de usuario de prueba de Deputy](#creating-a-deputy-test-user)**: para tener un homólogo de Britta Simon en Deputy que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2dc9d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2dc9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2dc9d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dc9d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2dc9d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Deputy.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="2dc9d-150">**Para configurar el inicio de sesión único de Azure AD con Deputy, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2dc9d-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="2dc9d-151">En Azure Portal, en la página de integración de la aplicación **Deputy**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2dc9d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="2dc9d-155">En la sección **Dominio y direcciones URL de Deputy**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="2dc9d-157">a.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-157">a.</span></span> <span data-ttu-id="2dc9d-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="2dc9d-159">b.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-159">b.</span></span> <span data-ttu-id="2dc9d-160">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="2dc9d-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2dc9d-162">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="2dc9d-164">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<your-subdomain>.<region>.deputy.com`.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="2dc9d-165">El sufijo de la región de Deputy es opcional o debe usar uno de los siguientes: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="2dc9d-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2dc9d-166">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-166">These values are not real.</span></span> <span data-ttu-id="2dc9d-167">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2dc9d-168">Póngase en contacto con el [equipo de soporte técnico de Deputy](https://www.deputy.com/call-centers-customer-support-scheduling-software) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="2dc9d-169">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="2dc9d-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2dc9d-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2dc9d-173">En la sección **Configuración de Deputy**, haga clic en **Configurar Deputy** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2dc9d-174">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="2dc9d-176">Vaya a la siguiente dirección URL: [https://(su subdominio).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="2dc9d-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="2dc9d-177">Vaya a **Configuración de seguridad** y haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="2dc9d-179">En esta página de **configuración de seguridad** , siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="2dc9d-181">a.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-181">a.</span></span> <span data-ttu-id="2dc9d-182">Habilite el **inicio de sesión social**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="2dc9d-183">b.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-183">b.</span></span> <span data-ttu-id="2dc9d-184">Abra el certificado codificado en base 64 descargado de Azure Portal en el Bloc de notas, copie su contenido en el portapapeles y luego péguelo en el cuadro de texto **Certificado OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="2dc9d-185">c.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-185">c.</span></span> <span data-ttu-id="2dc9d-186">En el cuadro de texto Dirección URL de inicio de sesión único de SAML, escriba `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="2dc9d-187">d.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-187">d.</span></span> <span data-ttu-id="2dc9d-188">En el cuadro de texto Dirección URL de inicio de sesión único de SAML, reemplace `<your subdomain>` por el subdominio.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="2dc9d-189">e.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-189">e.</span></span> <span data-ttu-id="2dc9d-190">En el cuadro de texto Dirección URL de inicio de sesión único de SAML, reemplace `<saml sso url>` por la **dirección URL del servicio de inicio de sesión único de SAML que haya copiado desde Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="2dc9d-191">f.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-191">f.</span></span> <span data-ttu-id="2dc9d-192">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="2dc9d-193">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2dc9d-194">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2dc9d-195">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2dc9d-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2dc9d-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dc9d-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="2dc9d-197">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2dc9d-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2dc9d-199">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2dc9d-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2dc9d-200">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2dc9d-202">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2dc9d-204">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2dc9d-206">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2dc9d-208">a.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-208">a.</span></span> <span data-ttu-id="2dc9d-209">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2dc9d-210">b.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-210">b.</span></span> <span data-ttu-id="2dc9d-211">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2dc9d-212">c.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-212">c.</span></span> <span data-ttu-id="2dc9d-213">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2dc9d-214">d.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-214">d.</span></span> <span data-ttu-id="2dc9d-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="2dc9d-216">Creación de usuario de prueba de Deputy</span><span class="sxs-lookup"><span data-stu-id="2dc9d-216">Creating a Deputy test user</span></span>

<span data-ttu-id="2dc9d-217">Para permitir que los usuarios de Azure AD inicien sesión en Deputy, deben aprovisionarse en Deputy.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="2dc9d-218">En el caso de Deputy, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="2dc9d-219">Para aprovisionar una cuenta de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2dc9d-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="2dc9d-220">Inicie sesión en su sitio de la compañía de Deputy como administrador.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="2dc9d-221">En la parte superior del panel de navegación, haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="2dc9d-222">![Personas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="2dc9d-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="2dc9d-223">Haga clic en el botón **Agregar personas** y en **Agregar una sola persona**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="2dc9d-224">![Agregar personas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Agregar personas")</span><span class="sxs-lookup"><span data-stu-id="2dc9d-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="2dc9d-225">Realice los pasos siguientes y haga clic en **Guardar e invitar**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="2dc9d-226">![Nuevo usuario](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="2dc9d-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="2dc9d-227">a.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-227">a.</span></span> <span data-ttu-id="2dc9d-228">En el cuadro de texto **Nombre**, escriba el nombre de un usuario, por ejemplo, **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="2dc9d-229">b.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-229">b.</span></span> <span data-ttu-id="2dc9d-230">En el cuadro de texto **Correo electrónico** , escriba la dirección de correo electrónico de la cuenta de Azure AD que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="2dc9d-231">c.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-231">c.</span></span> <span data-ttu-id="2dc9d-232">En el cuadro de texto **Trabaja en**, escriba el nombre de la empresa.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="2dc9d-233">d.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-233">d.</span></span> <span data-ttu-id="2dc9d-234">Haga clic en el botón **Guardar e invitar**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="2dc9d-235">El titular de la cuenta de AAD recibe un mensaje de correo y sigue un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="2dc9d-236">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Deputy que proporcione Deputy para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2dc9d-237">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dc9d-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2dc9d-238">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Deputy.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2dc9d-240">**Para asignar a Britta Simon a Deputy, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2dc9d-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="2dc9d-241">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2dc9d-243">En la lista de aplicaciones, seleccione **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-243">In the applications list, select **Deputy**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="2dc9d-245">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2dc9d-247">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-247">Click **Add** button.</span></span> <span data-ttu-id="2dc9d-248">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2dc9d-250">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2dc9d-251">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2dc9d-252">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2dc9d-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2dc9d-253">Testing single sign-on</span></span>

<span data-ttu-id="2dc9d-254">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="2dc9d-255">Al hacer clic en el icono de Deputy en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Deputy.</span><span class="sxs-lookup"><span data-stu-id="2dc9d-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2dc9d-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2dc9d-256">Additional resources</span></span>

* [<span data-ttu-id="2dc9d-257">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dc9d-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2dc9d-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2dc9d-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

