---
title: "Tutorial: Integración de Azure Active Directory con Nexonia | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="78546-103">Tutorial: Integración de Azure Active Directory con Nexonia</span><span class="sxs-lookup"><span data-stu-id="78546-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="78546-104">En este tutorial, obtendrá información sobre cómo integrar Nexonia con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78546-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78546-105">Integrar Nexonia con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="78546-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78546-106">Puede controlar en Azure AD quién tiene acceso a Nexonia</span><span class="sxs-lookup"><span data-stu-id="78546-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="78546-107">Puede permitir que los usuarios inicien sesión automáticamente en Nexonia (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78546-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78546-108">Puede administrar las cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="78546-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78546-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="78546-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="78546-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="78546-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78546-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="78546-111">Prerequisites</span></span>

<span data-ttu-id="78546-112">Para configurar la integración de Azure AD con Nexonia, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="78546-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="78546-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78546-113">An Azure AD subscription</span></span>
- <span data-ttu-id="78546-114">Una suscripción habilitada para el inicio de sesión único en Nexonia</span><span class="sxs-lookup"><span data-stu-id="78546-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78546-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="78546-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78546-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="78546-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78546-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="78546-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78546-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78546-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78546-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="78546-119">Scenario description</span></span>
<span data-ttu-id="78546-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="78546-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78546-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="78546-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78546-122">Incorporación de Nexonia desde la galería</span><span class="sxs-lookup"><span data-stu-id="78546-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="78546-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78546-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="78546-124">Incorporación de Nexonia desde la galería</span><span class="sxs-lookup"><span data-stu-id="78546-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="78546-125">Para configurar la integración de Nexonia en Azure AD, tendrá que agregar Nexonia desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="78546-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78546-126">**Para agregar Nexonia desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="78546-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78546-127">En **[Azure Portal](https://portal.azure.com)**, en el panel de navegación izquierdo, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78546-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78546-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="78546-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78546-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="78546-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="78546-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="78546-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="78546-134">En el cuadro de búsqueda, escriba **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="78546-134">In the search box, type **Nexonia**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="78546-136">En el panel de resultados, seleccione **Nexonia** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78546-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78546-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78546-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78546-139">En esta sección podrá configurar y probar el inicio de sesión único de Azure AD con Nexonia con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="78546-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="78546-140">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Nexonia para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78546-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="78546-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Nexonia.</span><span class="sxs-lookup"><span data-stu-id="78546-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="78546-142">Para establecer la relación de vínculo, en Nexonia, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="78546-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78546-143">Para configurar y probar el inicio de sesión único de Azure AD con Nexonia, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="78546-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78546-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="78546-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78546-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78546-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78546-146">**[Creación de un usuario de prueba de Nexonia](#creating-a-nexonia-test-user)**: para tener un homólogo de Britta Simon en Nexonia que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="78546-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78546-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78546-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78546-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="78546-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78546-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78546-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78546-150">En esta sección se habilita el inicio de sesión único de Azure AD en Azure Portal y se configura el inicio de sesión único en la aplicación Nexonia.</span><span class="sxs-lookup"><span data-stu-id="78546-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="78546-151">Si tiene problemas en la integración, vaya a este [vínculo](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) para consultar la guía de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="78546-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="78546-152">Si todavía no ha encontrado la solución, realice una solicitud de soporte técnico desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="78546-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="78546-153">**Para configurar el inicio de sesión único de Azure AD con Nexonia, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="78546-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="78546-154">En Azure Portal, en la página de integración de la aplicación **Nexonia**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="78546-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="78546-156">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="78546-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="78546-158">En la sección **Dominio y direcciones URL de Nexonia**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78546-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="78546-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`.</span><span class="sxs-lookup"><span data-stu-id="78546-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78546-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="78546-161">This value is not real.</span></span> <span data-ttu-id="78546-162">Actualice este valor con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="78546-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="78546-163">Póngase en contacto con el [equipo de soporte técnico de Nexonia](https://nexonia.zendesk.com/hc/requests/new) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="78546-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="78546-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="78546-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="78546-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="78546-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78546-168">En la sección **Configuración de Nexonia**, haga clic en **Configurar Nexonia** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="78546-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="78546-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="78546-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="78546-171">Para configurar el inicio de sesión único para la aplicación, póngase en contacto con el [equipo de soporte técnico de Nexonia](https://nexonia.zendesk.com/hc/requests/new) y proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78546-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="78546-172">• El **certificado**</span><span class="sxs-lookup"><span data-stu-id="78546-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="78546-173">• El **identificador de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="78546-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="78546-174">• La **URL del servicio de inicio de sesión único de SAML**</span><span class="sxs-lookup"><span data-stu-id="78546-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="78546-175">• La **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="78546-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="78546-176">Ahora puede leer una versión concisa de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78546-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78546-177">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="78546-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78546-178">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78546-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78546-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78546-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="78546-180">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="78546-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="78546-182">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="78546-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78546-183">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78546-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78546-185">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="78546-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78546-187">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="78546-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78546-189">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="78546-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78546-191">a.</span><span class="sxs-lookup"><span data-stu-id="78546-191">a.</span></span> <span data-ttu-id="78546-192">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78546-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78546-193">b.</span><span class="sxs-lookup"><span data-stu-id="78546-193">b.</span></span> <span data-ttu-id="78546-194">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78546-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78546-195">c.</span><span class="sxs-lookup"><span data-stu-id="78546-195">c.</span></span> <span data-ttu-id="78546-196">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="78546-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78546-197">d.</span><span class="sxs-lookup"><span data-stu-id="78546-197">d.</span></span> <span data-ttu-id="78546-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="78546-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="78546-199">Creación de un usuario de prueba de Nexonia</span><span class="sxs-lookup"><span data-stu-id="78546-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="78546-200">En esta sección, creará un usuario llamado Britta Simon en Nexonia.</span><span class="sxs-lookup"><span data-stu-id="78546-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="78546-201">Colabore con el [equipo de soporte técnico de Nexonia](https://nexonia.zendesk.com/hc/requests/new) para agregar los usuarios en la plataforma de Nexonia.</span><span class="sxs-lookup"><span data-stu-id="78546-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="78546-202">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="78546-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78546-203">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78546-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78546-204">En esta sección se habilita a Britta Simon para que use el inicio de sesión único de Azure al concederle acceso a Nexonia.</span><span class="sxs-lookup"><span data-stu-id="78546-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="78546-206">**Para asignar Britta Simon a Nexonia, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="78546-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="78546-207">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="78546-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="78546-209">En la lista de aplicaciones, seleccione **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="78546-209">In the applications list, select **Nexonia**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="78546-211">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="78546-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="78546-213">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="78546-213">Click **Add** button.</span></span> <span data-ttu-id="78546-214">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="78546-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="78546-216">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="78546-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78546-217">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="78546-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78546-218">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="78546-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78546-219">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="78546-219">Testing single sign-on</span></span>

<span data-ttu-id="78546-220">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="78546-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="78546-221">Al hacer clic en el icono de Nexonia en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Nexonia.</span><span class="sxs-lookup"><span data-stu-id="78546-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="78546-222">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="78546-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78546-223">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="78546-223">Additional resources</span></span>

* [<span data-ttu-id="78546-224">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78546-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78546-225">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78546-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

