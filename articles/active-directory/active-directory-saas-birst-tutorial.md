---
title: "Tutorial: Integración de Azure Active Directory con Birst Agile Business Analytics | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Birst Agile Business Analytics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 779f9e0a57ffb2274ea22a90ed9759734ab6916d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="63abb-103">Tutorial: Integración de Azure Active Directory con Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="63abb-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="63abb-104">En este tutorial, aprenderá a integrar Birst Agile Business Analytics con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63abb-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63abb-105">Integrar Birst Agile Business Analytics con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="63abb-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63abb-106">Puede controlar en Azure AD quién tiene acceso a Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="63abb-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="63abb-107">Puede permitir que los usuarios inicien sesión automáticamente en Birst Agile Business Analytics (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63abb-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63abb-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="63abb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="63abb-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63abb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63abb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="63abb-110">Prerequisites</span></span>

<span data-ttu-id="63abb-111">Para configurar la integración de Azure AD con Birst Agile Business Analytics, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="63abb-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="63abb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63abb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63abb-113">Una suscripción habilitada al inicio de sesión único de Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="63abb-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63abb-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="63abb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63abb-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="63abb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63abb-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="63abb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63abb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63abb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63abb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="63abb-118">Scenario description</span></span>
<span data-ttu-id="63abb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="63abb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63abb-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="63abb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63abb-121">Adición de Birst Agile Business Analytics desde la galería</span><span class="sxs-lookup"><span data-stu-id="63abb-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="63abb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63abb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="63abb-123">Adición de Birst Agile Business Analytics desde la galería</span><span class="sxs-lookup"><span data-stu-id="63abb-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="63abb-124">Para configurar la integración de Birst Agile Business Analytics en Azure AD, es preciso agregar Birst Agile Business Analytics desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="63abb-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63abb-125">**Para agregar Birst Agile Business Analytics desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="63abb-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63abb-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63abb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="63abb-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="63abb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63abb-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63abb-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="63abb-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63abb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="63abb-133">En el cuadro de búsqueda, escriba **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="63abb-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="63abb-135">En el panel de resultados, seleccione **Birst Agile Business Analytics** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="63abb-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63abb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63abb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63abb-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con Birst Agile Business ByDesign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="63abb-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="63abb-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Birst Agile Business Analytics para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63abb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="63abb-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="63abb-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="63abb-141">Para establecer la relación de vínculo, en Business Analytics, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="63abb-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="63abb-142">Para configurar y probar el inicio de sesión único de Azure AD con Birst Agile Business Analytics, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="63abb-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63abb-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="63abb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="63abb-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63abb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63abb-145">**[Creación de un usuario de prueba de Birst Agile Business Analytics](#creating-a-birst-agile-business-analytics-test-user)**: para tener un homólogo de Britta Simon en Birst Agile Business Analytics que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63abb-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="63abb-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63abb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63abb-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="63abb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63abb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63abb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63abb-149">El objetivo de esta sección es habilitar el inicio de sesión único de Azure AD en Azure Portal y configurar el inicio de sesión único en la aplicación Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="63abb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="63abb-150">**Para configurar el inicio de sesión único de Azure AD con Birst Agile Business Analytics, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="63abb-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="63abb-151">En Azure Portal, en la página de integración de la aplicación **** , haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="63abb-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="63abb-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="63abb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="63abb-155">En la sección **Dominio y direcciones URL de Birst Agile Business Analytics**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="63abb-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="63abb-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`.</span><span class="sxs-lookup"><span data-stu-id="63abb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="63abb-158">La dirección URL depende del centro de datos en el que se encuentre la cuenta de Birst:</span><span class="sxs-lookup"><span data-stu-id="63abb-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="63abb-159">En el centro de datos de EE.UU., siga este patrón: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="63abb-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="63abb-160">En el centro de datos de Europa, siga este patrón: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="63abb-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63abb-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="63abb-161">This value is not real.</span></span> <span data-ttu-id="63abb-162">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="63abb-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="63abb-163">Póngase en contacto con el [equipo de soporte al cliente de Birst Agile Business Analytics](mailto:info@birst.com) para obtener el valor.</span><span class="sxs-lookup"><span data-stu-id="63abb-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
4. <span data-ttu-id="63abb-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="63abb-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="63abb-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="63abb-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63abb-168">En la sección **Configuración de Birst Agile Business Analytics**, haga clic en **Configurar Birst Agile Business Analytics** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="63abb-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="63abb-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="63abb-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="63abb-171">Para configurar el inicio de sesión único en el lado de **Birst Agile Business Analytics**, es preciso enviar los datos descargados de **Certificado (Base64)**, **Sign-Out URL (Dirección URL de cierre de sesión), SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Birst Agile Business Analytics](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="63abb-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="63abb-172">Indique al equipo de Birst que esta integración necesita el algoritmo SHA256 (no se admite SHA1) para que pueda establecer el SSO en el servidor adecuado, como **app2101**, etc.</span><span class="sxs-lookup"><span data-stu-id="63abb-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="63abb-173">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="63abb-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="63abb-174">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="63abb-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="63abb-175">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63abb-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63abb-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63abb-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="63abb-177">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="63abb-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="63abb-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="63abb-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63abb-180">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63abb-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63abb-182">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="63abb-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63abb-184">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63abb-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63abb-186">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="63abb-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63abb-188">a.</span><span class="sxs-lookup"><span data-stu-id="63abb-188">a.</span></span> <span data-ttu-id="63abb-189">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63abb-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63abb-190">b.</span><span class="sxs-lookup"><span data-stu-id="63abb-190">b.</span></span> <span data-ttu-id="63abb-191">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63abb-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63abb-192">c.</span><span class="sxs-lookup"><span data-stu-id="63abb-192">c.</span></span> <span data-ttu-id="63abb-193">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="63abb-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="63abb-194">d.</span><span class="sxs-lookup"><span data-stu-id="63abb-194">d.</span></span> <span data-ttu-id="63abb-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="63abb-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="63abb-196">Creación de un usuario de prueba de Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="63abb-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="63abb-197">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="63abb-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="63abb-198">Trabaje con el [equipo de soporte técnico de Birst Agile Business Analytics](mailto:info@birst.com) para agregar los usuarios de la cuenta de Birst.</span><span class="sxs-lookup"><span data-stu-id="63abb-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="63abb-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63abb-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="63abb-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure, para lo que le concede acceso a Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="63abb-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="63abb-202">**Para asignar Britta Simon a Birst Agile Business Analytics, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="63abb-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="63abb-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63abb-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="63abb-205">En la lista de aplicaciones, seleccione **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="63abb-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="63abb-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63abb-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="63abb-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="63abb-209">Click **Add** button.</span></span> <span data-ttu-id="63abb-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63abb-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="63abb-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="63abb-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="63abb-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63abb-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63abb-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63abb-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63abb-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="63abb-215">Testing single sign-on</span></span>

<span data-ttu-id="63abb-216">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="63abb-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="63abb-217">Al hacer clic en el icono de Birst Agile Business Analytics en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="63abb-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="63abb-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="63abb-218">Additional resources</span></span>

* [<span data-ttu-id="63abb-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63abb-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63abb-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63abb-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

