---
title: "Tutorial: Integración de Azure Active Directory con SpringCM | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: edfd06a06c730597fee4569ca1ce29092b45244a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="e4172-103">Tutorial: integración de Azure Active Directory con SprinkCM</span><span class="sxs-lookup"><span data-stu-id="e4172-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="e4172-104">En este tutorial, obtendrá información sobre cómo integrar SpringCM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e4172-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4172-105">La integración de SpringCM con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e4172-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e4172-106">Puede controlar en Azure AD quién tiene acceso a SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e4172-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="e4172-107">Puede permitir que los usuarios inicien sesión automáticamente en SpringCM (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4172-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4172-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4172-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e4172-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e4172-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4172-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e4172-110">Prerequisites</span></span>

<span data-ttu-id="e4172-111">Para configurar la integración de Azure AD con SpringCM, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e4172-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="e4172-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4172-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4172-113">Una suscripción habilitada para el inicio de sesión único en SpringCM</span><span class="sxs-lookup"><span data-stu-id="e4172-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4172-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e4172-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4172-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e4172-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4172-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e4172-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4172-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4172-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4172-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e4172-118">Scenario description</span></span>
<span data-ttu-id="e4172-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e4172-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4172-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e4172-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4172-121">Agregar SpringCM desde la galería</span><span class="sxs-lookup"><span data-stu-id="e4172-121">Adding SpringCM from the gallery</span></span>
2. <span data-ttu-id="e4172-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4172-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="e4172-123">Agregar SpringCM desde la galería</span><span class="sxs-lookup"><span data-stu-id="e4172-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="e4172-124">Para configurar la integración de SpringCM en Azure AD, deberá agregar SpringCM desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e4172-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e4172-125">**Para agregar SpringCM desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e4172-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e4172-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4172-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4172-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e4172-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e4172-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e4172-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e4172-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e4172-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e4172-133">En el cuadro de búsqueda, escriba **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="e4172-133">In the search box, type **SpringCM**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="e4172-135">En el panel de resultados, seleccione **SpringCM** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4172-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4172-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4172-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4172-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SpringCM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e4172-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e4172-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SpringCM para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4172-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="e4172-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e4172-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="e4172-141">Para establecer la relación de vínculo, en SpringCM, asigne el valor del **nombre de usuario** de Azure AD como el valor del **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e4172-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e4172-142">Para configurar y probar el inicio de sesión único de Azure AD con SpringCM, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e4172-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e4172-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e4172-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e4172-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4172-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4172-145">**[Creación de un usuario de prueba de SpringCM](#creating-a-springcm-test-user)**: para tener un homólogo de Britta Simon en SpringCM vinculado a la representación del usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4172-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e4172-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4172-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4172-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e4172-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4172-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4172-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4172-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e4172-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="e4172-150">**Para configurar el inicio de sesión único de Azure AD con SpringCM, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="e4172-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="e4172-151">En Azure Portal, en la página de integración de la aplicación **SpringCM**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e4172-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e4172-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e4172-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="e4172-155">En la sección **Dominio y direcciones URL de SpringCM**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4172-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="e4172-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`.</span><span class="sxs-lookup"><span data-stu-id="e4172-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e4172-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="e4172-158">This value is not real.</span></span> <span data-ttu-id="e4172-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="e4172-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e4172-160">Póngase en contacto con el [equipo de soporte técnico de SpringCM](https://knowledge.springcm.com/support) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="e4172-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
4. <span data-ttu-id="e4172-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (sin procesar)** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e4172-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="e4172-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e4172-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e4172-165">En la sección **Configuración de SpringCM**, haga clic en **Configurar SpringCM** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e4172-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e4172-166">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y Dirección URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="e4172-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="e4172-168">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de **SpringCM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e4172-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="e4172-169">En el menú de la parte superior, haga clic en**IR A**, haga clic en **Preferencias** y, luego, en la sección **Preferencias de cuenta**, haga clic en**SSO de SAML**.</span><span class="sxs-lookup"><span data-stu-id="e4172-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="e4172-170">![SSO DE SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SSO DE SAML")</span><span class="sxs-lookup"><span data-stu-id="e4172-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="e4172-171">En la sección de configuración del proveedor de identidades, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4172-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="e4172-172">![Configuración del proveedor de identidades](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Configuración del proveedor de identidades")</span><span class="sxs-lookup"><span data-stu-id="e4172-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="e4172-173">a.</span><span class="sxs-lookup"><span data-stu-id="e4172-173">a.</span></span> <span data-ttu-id="e4172-174">Para cargar el certificado descargado de Azure Active Directory, haga clic en **Seleccionar certificado de emisor** o **Cambiar el certificado del emisor**.</span><span class="sxs-lookup"><span data-stu-id="e4172-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="e4172-175">b.</span><span class="sxs-lookup"><span data-stu-id="e4172-175">b.</span></span> <span data-ttu-id="e4172-176">Pegue el valor del **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **Issuer** (Emisor).</span><span class="sxs-lookup"><span data-stu-id="e4172-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="e4172-177">c.</span><span class="sxs-lookup"><span data-stu-id="e4172-177">c.</span></span> <span data-ttu-id="e4172-178">Pegue la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal en el cuadro de texto **Service Provider (SP) Initiated Endpoint** (Punto de conexión del proveedor de servicios iniciado).</span><span class="sxs-lookup"><span data-stu-id="e4172-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="e4172-179">d.</span><span class="sxs-lookup"><span data-stu-id="e4172-179">d.</span></span> <span data-ttu-id="e4172-180">Seleccione **SAML Enabled** (SAML habilitado) como **Enable** (Habilitar).</span><span class="sxs-lookup"><span data-stu-id="e4172-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="e4172-181">e.</span><span class="sxs-lookup"><span data-stu-id="e4172-181">e.</span></span> <span data-ttu-id="e4172-182">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e4172-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="e4172-183">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4172-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e4172-184">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e4172-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e4172-185">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e4172-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4172-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4172-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4172-187">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e4172-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e4172-189">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e4172-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e4172-190">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4172-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4172-192">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e4172-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4172-194">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e4172-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4172-196">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e4172-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4172-198">a.</span><span class="sxs-lookup"><span data-stu-id="e4172-198">a.</span></span> <span data-ttu-id="e4172-199">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e4172-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4172-200">b.</span><span class="sxs-lookup"><span data-stu-id="e4172-200">b.</span></span> <span data-ttu-id="e4172-201">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4172-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4172-202">c.</span><span class="sxs-lookup"><span data-stu-id="e4172-202">c.</span></span> <span data-ttu-id="e4172-203">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e4172-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e4172-204">d.</span><span class="sxs-lookup"><span data-stu-id="e4172-204">d.</span></span> <span data-ttu-id="e4172-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e4172-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="e4172-206">Creación de un usuario de prueba de SpringCM</span><span class="sxs-lookup"><span data-stu-id="e4172-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="e4172-207">Para permitir que los usuarios de Azure Active Directory inicien sesión en SpringCM, deben aprovisionarse en SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e4172-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="e4172-208">En el caso de SpringCM, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e4172-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e4172-209">Para obtener más información, consulte [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user) (Creación y edición de un usuario de SpringCM).</span><span class="sxs-lookup"><span data-stu-id="e4172-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="e4172-210">**Para aprovisionar cuentas de usuario en SpringCM, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="e4172-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="e4172-211">Inicie sesión en su sitio de compañía de **SpringCM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e4172-211">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="e4172-212">Haga clic en **GOTO** y, luego, en **ADDRESS BOOK** (LIBRETA DE DIRECCIONES).</span><span class="sxs-lookup"><span data-stu-id="e4172-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="e4172-213">![Creación de usuarios](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="e4172-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="e4172-214">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="e4172-214">Click **Create User**.</span></span>

4. <span data-ttu-id="e4172-215">Seleccione un **Rol de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e4172-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="e4172-216">Seleccione **Enviar correo electrónico de activación**.</span><span class="sxs-lookup"><span data-stu-id="e4172-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="e4172-217">Escriba el nombre, el apellido y la dirección de correo electrónico de una cuenta de usuario de Azure Active Directory válida que quiera aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="e4172-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="e4172-218">Agregue el usuario a un **Grupo de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e4172-218">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="e4172-219">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="e4172-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="e4172-220">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de SpringCM ofrecida por SpringCM para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="e4172-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e4172-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4172-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e4172-222">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e4172-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e4172-224">**Para asignar el usuario Britta Simon a SpringCM, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e4172-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="e4172-225">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e4172-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e4172-227">En la lista de aplicaciones, seleccione **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="e4172-227">In the applications list, select **SpringCM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="e4172-229">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e4172-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e4172-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e4172-231">Click **Add** button.</span></span> <span data-ttu-id="e4172-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e4172-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e4172-234">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e4172-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e4172-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e4172-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4172-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e4172-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4172-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e4172-237">Testing single sign-on</span></span>

<span data-ttu-id="e4172-238">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e4172-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="e4172-239">Al hacer clic en el icono de SpringCM en el panel de acceso, debería iniciar sesión automáticamente en su aplicación SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e4172-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="e4172-240">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e4172-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e4172-241">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e4172-241">Additional resources</span></span>

* [<span data-ttu-id="e4172-242">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4172-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4172-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e4172-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

