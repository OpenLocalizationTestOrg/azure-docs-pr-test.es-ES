---
title: "Tutorial: Integración de Azure Active Directory con Menlo Security | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Menlo Security."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="68172-103">Tutorial: Integración de Azure Active Directory con Menlo Security</span><span class="sxs-lookup"><span data-stu-id="68172-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="68172-104">En este tutorial, aprenderá a integrar Menlo Security con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68172-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68172-105">Integrar Menlo Security con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="68172-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="68172-106">Puede controlar en Azure AD quién tiene acceso a Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="68172-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="68172-107">Puede permitir que los usuarios inicien sesión automáticamente en Menlo Security (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68172-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68172-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="68172-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="68172-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="68172-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="68172-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="68172-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68172-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="68172-111">Prerequisites</span></span>

<span data-ttu-id="68172-112">Para configurar la integración de Azure AD con Menlo Security, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="68172-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="68172-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="68172-113">An Azure AD subscription</span></span>
- <span data-ttu-id="68172-114">Una suscripción habilitada para el inicio de sesión único en Menlo Security</span><span class="sxs-lookup"><span data-stu-id="68172-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68172-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="68172-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68172-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="68172-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68172-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="68172-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68172-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68172-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68172-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="68172-119">Scenario description</span></span>
<span data-ttu-id="68172-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="68172-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68172-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="68172-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68172-122">Adición de Menlo Security desde la galería</span><span class="sxs-lookup"><span data-stu-id="68172-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="68172-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="68172-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="68172-124">Adición de Menlo Security desde la galería</span><span class="sxs-lookup"><span data-stu-id="68172-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="68172-125">Para configurar la integración de Menlo Security en Azure AD, debe agregar Menlo Security desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="68172-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="68172-126">**Para agregar Menlo Security desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="68172-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="68172-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68172-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68172-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="68172-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="68172-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="68172-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="68172-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68172-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="68172-134">En el cuadro de búsqueda, escriba **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="68172-134">In the search box, type **Menlo Security**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="68172-136">En el panel de resultados, seleccione **Menlo Security** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="68172-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68172-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="68172-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68172-139">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Menlo Security con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="68172-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68172-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Menlo Security para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68172-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="68172-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="68172-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="68172-142">Para establecer esta relación de vínculo, se toma el valor del **nombre de usuario** en Azure AD y se asigna como valor del **nombre de usuario** en Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="68172-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="68172-143">Para configurar y probar el inicio de sesión único de Azure AD con Menlo Security, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="68172-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="68172-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="68172-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="68172-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68172-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68172-146">**[Creación de un usuario de prueba de Menlo Security](#creating-a-menlo-security-test-user)**: para tener un homólogo de Britta Simon en Menlo Security que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68172-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="68172-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68172-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68172-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="68172-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68172-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="68172-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68172-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="68172-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="68172-151">**Para configurar el inicio de sesión único de Azure AD con Menlo Security, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="68172-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="68172-152">En Azure Portal, en la página de integración de la aplicación **Menlo Security**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="68172-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="68172-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="68172-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="68172-156">En la sección **Dominio y direcciones URL de Menlo Security**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="68172-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="68172-158">a.</span><span class="sxs-lookup"><span data-stu-id="68172-158">a.</span></span> <span data-ttu-id="68172-159">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.menlosecurity.com/account/login`.</span><span class="sxs-lookup"><span data-stu-id="68172-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="68172-160">b.</span><span class="sxs-lookup"><span data-stu-id="68172-160">b.</span></span> <span data-ttu-id="68172-161">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="68172-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="68172-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="68172-162">These values are not the real.</span></span> <span data-ttu-id="68172-163">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="68172-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="68172-164">Póngase en contacto con el [equipo de soporte de cliente de Menlo Security](https://www.menlosecurity.com/menlo-contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="68172-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="68172-165">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="68172-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="68172-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="68172-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="68172-169">En la sección **Configuración de Menlo Security**, haga clic en **Configurar Menlo Security** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="68172-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="68172-170">Copie el **Identificador de entidad en SAML** y la **Dirección URL de inicio de sesión único de SAML** de la **sección Referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="68172-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="68172-172">Para configurar el inicio de sesión único en **Menlo Security**, regístrese en el sitio web de **Menlo Security** como administrador.</span><span class="sxs-lookup"><span data-stu-id="68172-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="68172-173">En **Settings** (Configuración), vaya a **Authentication** (Autenticación) y realice las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="68172-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="68172-175">a.</span><span class="sxs-lookup"><span data-stu-id="68172-175">a.</span></span> <span data-ttu-id="68172-176">Active la casilla **Enable user authentication using SAML** (Habilitar la autenticación de usuario mediante SAML).</span><span class="sxs-lookup"><span data-stu-id="68172-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="68172-177">b.</span><span class="sxs-lookup"><span data-stu-id="68172-177">b.</span></span> <span data-ttu-id="68172-178">Seleccione **Allow External Access** (Permitir acceso externo) en **Yes** (Sí).</span><span class="sxs-lookup"><span data-stu-id="68172-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="68172-179">c.</span><span class="sxs-lookup"><span data-stu-id="68172-179">c.</span></span> <span data-ttu-id="68172-180">En **SAML Provider** (Proveedor de SAML), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68172-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="68172-181">d.</span><span class="sxs-lookup"><span data-stu-id="68172-181">d.</span></span> <span data-ttu-id="68172-182">**SAML 2.0 Endpoint** (Punto de conexión de SAML 2.0): copie la **Dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="68172-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="68172-183">e.</span><span class="sxs-lookup"><span data-stu-id="68172-183">e.</span></span> <span data-ttu-id="68172-184">**Service Identifier (Issuer)** (Identificador del servicio [emisor]): copie el **Identificador de entidad en SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="68172-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="68172-185">f.</span><span class="sxs-lookup"><span data-stu-id="68172-185">f.</span></span> <span data-ttu-id="68172-186">**X.509 Certificate** (Certificado X.509): abra el **Certificado (Base64)** descargado de Azure Portal en el Bloc de notas y péguelo en este cuadro.</span><span class="sxs-lookup"><span data-stu-id="68172-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="68172-187">g.</span><span class="sxs-lookup"><span data-stu-id="68172-187">g.</span></span> <span data-ttu-id="68172-188">Haga clic en **Guardar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="68172-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="68172-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="68172-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="68172-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="68172-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68172-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68172-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68172-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="68172-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="68172-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="68172-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="68172-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="68172-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="68172-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68172-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68172-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="68172-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68172-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68172-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68172-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="68172-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68172-204">a.</span><span class="sxs-lookup"><span data-stu-id="68172-204">a.</span></span> <span data-ttu-id="68172-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68172-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68172-206">b.</span><span class="sxs-lookup"><span data-stu-id="68172-206">b.</span></span> <span data-ttu-id="68172-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68172-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68172-208">c.</span><span class="sxs-lookup"><span data-stu-id="68172-208">c.</span></span> <span data-ttu-id="68172-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="68172-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="68172-210">d.</span><span class="sxs-lookup"><span data-stu-id="68172-210">d.</span></span> <span data-ttu-id="68172-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="68172-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="68172-212">Creación de un usuario de prueba de Menlo Security</span><span class="sxs-lookup"><span data-stu-id="68172-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="68172-213">En esta sección, creará un usuario llamado Britta Simon en Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="68172-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="68172-214">Colabore con el [equipo de soporte de cliente de Menlo Security](https://www.menlosecurity.com/menlo-contact) para agregar los usuarios a la plataforma de Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="68172-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="68172-215">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="68172-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="68172-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="68172-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="68172-217">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="68172-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="68172-219">**Para asignar Britta Simon a Menlo Security, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="68172-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="68172-220">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="68172-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="68172-222">En la lista de aplicaciones, seleccione **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="68172-222">In the applications list, select **Menlo Security**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="68172-224">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="68172-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="68172-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="68172-226">Click **Add** button.</span></span> <span data-ttu-id="68172-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="68172-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="68172-229">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="68172-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="68172-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="68172-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68172-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="68172-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68172-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="68172-232">Testing single sign-on</span></span>

<span data-ttu-id="68172-233">En esta sección, probará la configuración de inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68172-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="68172-234">Abra una ventana del explorador en modo "InPrivate" o "Incognito" para desencadenar una nueva autenticación.</span><span class="sxs-lookup"><span data-stu-id="68172-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="68172-235">En Internet Explorer, utilice Ctrl + Mayús + P.</span><span class="sxs-lookup"><span data-stu-id="68172-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="68172-236">En Chrome, utilice Ctrl + Mayús + N.</span><span class="sxs-lookup"><span data-stu-id="68172-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="68172-237">En la ventana de exploración privada, vaya a un recurso protegido e inicie sesión en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68172-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="68172-238">Cuando inicie sesión correctamente, se le llevará al sitio solicitado en una sesión de aislamiento.</span><span class="sxs-lookup"><span data-stu-id="68172-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68172-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="68172-239">Additional resources</span></span>

* [<span data-ttu-id="68172-240">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68172-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68172-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68172-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

