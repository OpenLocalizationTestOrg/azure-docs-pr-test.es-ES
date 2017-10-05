---
title: "Tutorial: integración de Azure Active Directory con Jitbit Helpdesk | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="31a2c-103">Tutorial: Integración de Azure Active Directory con Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="31a2c-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="31a2c-104">En este tutorial, obtendrá información sobre cómo integrar Jitbit Helpdesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31a2c-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31a2c-105">La integración de Jitbit Helpdesk con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="31a2c-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31a2c-106">Puede controlar en Azure AD quién tiene acceso a Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="31a2c-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="31a2c-107">Puede permitir que los usuarios inicien sesión automáticamente en Jitbit Helpdesk (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a2c-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31a2c-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="31a2c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31a2c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31a2c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31a2c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="31a2c-110">Prerequisites</span></span>

<span data-ttu-id="31a2c-111">Para configurar la integración de Azure AD con Jitbit Helpdesk, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="31a2c-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="31a2c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a2c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31a2c-113">Una suscripción habilitada para el inicio de sesión único en Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="31a2c-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31a2c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="31a2c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31a2c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="31a2c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31a2c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="31a2c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31a2c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31a2c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31a2c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="31a2c-118">Scenario description</span></span>
<span data-ttu-id="31a2c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="31a2c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31a2c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="31a2c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31a2c-121">Incorporación de Jitbit Helpdesk desde la Galería</span><span class="sxs-lookup"><span data-stu-id="31a2c-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="31a2c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a2c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="31a2c-123">Incorporación de Jitbit Helpdesk desde la Galería</span><span class="sxs-lookup"><span data-stu-id="31a2c-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="31a2c-124">Para configurar la integración de Jitbit Helpdesk en Azure AD, será preciso que agregue Jitbit Helpdesk desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="31a2c-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31a2c-125">**Para agregar Jitbit Helpdesk desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="31a2c-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31a2c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31a2c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31a2c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="31a2c-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31a2c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="31a2c-133">En el cuadro de búsqueda, escriba **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="31a2c-135">En el panel de resultados, seleccione **Jitbit Helpdesk** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31a2c-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31a2c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a2c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31a2c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jitbit Helpdesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="31a2c-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31a2c-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Jitbit Helpdesk para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31a2c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="31a2c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="31a2c-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="31a2c-141">Para establecer la relación de vínculo, en Jitbit Helpdesk, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31a2c-142">Para configurar y probar el inicio de sesión único de Azure AD con Jitbit Helpdesk, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="31a2c-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31a2c-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="31a2c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31a2c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31a2c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31a2c-145">**[Creación de un usuario de prueba de Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**: el objetivo es tener un homólogo de Britta Simon en Jitbit Helpdesk que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31a2c-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31a2c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31a2c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31a2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="31a2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31a2c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a2c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31a2c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="31a2c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="31a2c-150">**Para configurar el inicio de sesión único de Azure AD con Jitbit Helpdesk, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="31a2c-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="31a2c-151">En Azure Portal, en la página de integración de la aplicación **Jitbit Helpdesk**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="31a2c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31a2c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="31a2c-155">En la sección **Dominio y direcciones URL de Jitbit Helpdesk**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="31a2c-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="31a2c-157">a.</span><span class="sxs-lookup"><span data-stu-id="31a2c-157">a.</span></span> <span data-ttu-id="31a2c-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="31a2c-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="31a2c-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="31a2c-159">This value is not real.</span></span> <span data-ttu-id="31a2c-160">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="31a2c-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="31a2c-161">Póngase en contacto con el [equipo de soporte técnico de Jitbit Helpdesk](https://www.jitbit.com/support/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="31a2c-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="31a2c-162">b.</span><span class="sxs-lookup"><span data-stu-id="31a2c-162">b.</span></span>  <span data-ttu-id="31a2c-163">En el cuadro de texto **Identificador**, escriba una dirección URL como:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="31a2c-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="31a2c-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="31a2c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="31a2c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="31a2c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31a2c-168">En la sección **Configuración de Jitbit Helpdesk**, haga clic en **Configurar Jitbit Helpdesk** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31a2c-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="31a2c-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="31a2c-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="31a2c-172">En la barra de herramientas de la parte superior, haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="31a2c-173">![Administración](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="31a2c-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="31a2c-174">Haga clic en **Configuración general**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="31a2c-175">![Usuarios, compañías y permisos](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Usuarios, compañías y permisos")</span><span class="sxs-lookup"><span data-stu-id="31a2c-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="31a2c-176">En la sección **Configuración de autenticación** , realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="31a2c-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="31a2c-177">![Configuración de la autenticación](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Configuración de la autenticación")</span><span class="sxs-lookup"><span data-stu-id="31a2c-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="31a2c-178">a.</span><span class="sxs-lookup"><span data-stu-id="31a2c-178">a.</span></span> <span data-ttu-id="31a2c-179">Seleccione **Enable SAML 2.0 single sign on** (Habilitar inicio de sesión único de SAML 2.0) para iniciar sesión mediante inicio de sesión único (SSO) con **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="31a2c-180">b.</span><span class="sxs-lookup"><span data-stu-id="31a2c-180">b.</span></span> <span data-ttu-id="31a2c-181">En el cuadro de texto **EndPoint URL** (Dirección URL del punto de conexión), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="31a2c-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="31a2c-182">c.</span><span class="sxs-lookup"><span data-stu-id="31a2c-182">c.</span></span> <span data-ttu-id="31a2c-183">Abra el certificado codificado en **base-64** en el Bloc de notas, copie el contenido del mismo en el Portapapeles y péguelo en el cuadro de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="31a2c-184">d.</span><span class="sxs-lookup"><span data-stu-id="31a2c-184">d.</span></span> <span data-ttu-id="31a2c-185">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="31a2c-186">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31a2c-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31a2c-187">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="31a2c-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31a2c-188">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31a2c-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31a2c-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a2c-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="31a2c-190">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="31a2c-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="31a2c-192">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="31a2c-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31a2c-193">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31a2c-195">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31a2c-197">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31a2c-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31a2c-199">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="31a2c-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31a2c-201">a.</span><span class="sxs-lookup"><span data-stu-id="31a2c-201">a.</span></span> <span data-ttu-id="31a2c-202">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="31a2c-203">b.</span><span class="sxs-lookup"><span data-stu-id="31a2c-203">b.</span></span> <span data-ttu-id="31a2c-204">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31a2c-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31a2c-205">c.</span><span class="sxs-lookup"><span data-stu-id="31a2c-205">c.</span></span> <span data-ttu-id="31a2c-206">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31a2c-207">d.</span><span class="sxs-lookup"><span data-stu-id="31a2c-207">d.</span></span> <span data-ttu-id="31a2c-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="31a2c-209">Creación de un usuario de prueba de Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="31a2c-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="31a2c-210">Para permitir que los usuarios de Azure AD inicien sesión en Jitbit Helpdesk, deben aprovisionarse en Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="31a2c-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="31a2c-211">En el caso de Jitbit Helpdesk, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="31a2c-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="31a2c-212">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="31a2c-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="31a2c-213">Inicie sesión en su inquilino de **Jitbit Helpdesk** .</span><span class="sxs-lookup"><span data-stu-id="31a2c-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="31a2c-214">En el menú de la parte superior, haga clic en **Administration**(Administración).</span><span class="sxs-lookup"><span data-stu-id="31a2c-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="31a2c-215">![Administración](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="31a2c-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="31a2c-216">Haga clic en **Usuarios, compañías y permisos**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="31a2c-217">![Usuarios, compañías y permisos](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Usuarios, compañías y permisos")</span><span class="sxs-lookup"><span data-stu-id="31a2c-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="31a2c-218">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="31a2c-219">![Agregar usuario](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="31a2c-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="31a2c-220">En la sección Crear, escriba los datos de la cuenta de Azure AD que desee aprovisionar como sigue:</span><span class="sxs-lookup"><span data-stu-id="31a2c-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="31a2c-221">![Crear](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="31a2c-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="31a2c-222">a.</span><span class="sxs-lookup"><span data-stu-id="31a2c-222">a.</span></span> <span data-ttu-id="31a2c-223">En el cuadro de texto **Nombre de usuario**, escriba el nombre de usuario **Britta Simon** como en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="31a2c-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="31a2c-224">b.</span><span class="sxs-lookup"><span data-stu-id="31a2c-224">b.</span></span> <span data-ttu-id="31a2c-225">En el cuadro de texto **Correo electrónico**, escriba el correo electrónico del usuario, en el ejemplo  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="31a2c-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="31a2c-226">c.</span><span class="sxs-lookup"><span data-stu-id="31a2c-226">c.</span></span> <span data-ttu-id="31a2c-227">En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="31a2c-228">d.</span><span class="sxs-lookup"><span data-stu-id="31a2c-228">d.</span></span> <span data-ttu-id="31a2c-229">En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="31a2c-230">e.</span><span class="sxs-lookup"><span data-stu-id="31a2c-230">e.</span></span> <span data-ttu-id="31a2c-231">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="31a2c-232">Puede usar cualquier herramienta de creación de cuentas de usuario de Jitbit Helpdesk u otras API proporcionadas por Jitbit Helpdesk para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31a2c-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31a2c-233">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a2c-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31a2c-234">En esta sección, concederá acceso a Britta Simon a Jitbit Helpdesk para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="31a2c-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="31a2c-236">**Para asignar a Britta Simon a Jitbit Helpdesk, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="31a2c-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="31a2c-237">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="31a2c-239">En la lista de aplicaciones, seleccione **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="31a2c-241">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="31a2c-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-243">Click **Add** button.</span></span> <span data-ttu-id="31a2c-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="31a2c-246">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="31a2c-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31a2c-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31a2c-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31a2c-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31a2c-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="31a2c-249">Testing single sign-on</span></span>

<span data-ttu-id="31a2c-250">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="31a2c-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31a2c-251">Al hacer clic en el icono de Jitbit Helpdesk en el panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="31a2c-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="31a2c-252">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31a2c-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31a2c-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="31a2c-253">Additional resources</span></span>

* [<span data-ttu-id="31a2c-254">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31a2c-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31a2c-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31a2c-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

