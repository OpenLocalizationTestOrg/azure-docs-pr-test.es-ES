---
title: "Tutorial: Integración de Azure Active Directory con Freshdesk | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="efb5e-103">Tutorial: Integración de Azure Active Directory con Freshdesk</span><span class="sxs-lookup"><span data-stu-id="efb5e-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="efb5e-104">En este tutorial, obtendrá información sobre cómo integrar FreshDesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="efb5e-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efb5e-105">La integración de FreshDesk con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="efb5e-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="efb5e-106">En Azure AD se puede controlar quién tiene acceso a FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="efb5e-107">Puede permitir que los usuarios inicien sesión automáticamente en FreshDesk (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb5e-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="efb5e-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="efb5e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="efb5e-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="efb5e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efb5e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="efb5e-110">Prerequisites</span></span>

<span data-ttu-id="efb5e-111">Para configurar la integración de Azure AD con FreshDesk, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="efb5e-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="efb5e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efb5e-113">Una suscripción habilitada para el inicio de sesión único en FreshDesk</span><span class="sxs-lookup"><span data-stu-id="efb5e-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="efb5e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="efb5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="efb5e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="efb5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="efb5e-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="efb5e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="efb5e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efb5e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="efb5e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="efb5e-118">Scenario description</span></span>
<span data-ttu-id="efb5e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="efb5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="efb5e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="efb5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efb5e-121">Agregar FreshDesk desde la galería</span><span class="sxs-lookup"><span data-stu-id="efb5e-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="efb5e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="efb5e-123">Agregar FreshDesk desde la galería</span><span class="sxs-lookup"><span data-stu-id="efb5e-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="efb5e-124">Para configurar la integración de FreshDesk en Azure AD, deberá agregar FreshDesk desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="efb5e-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="efb5e-125">**Para agregar FreshDesk desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="efb5e-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="efb5e-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="efb5e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="efb5e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="efb5e-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="efb5e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="efb5e-133">En el cuadro de búsqueda, escriba **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-133">In the search box, type **FreshDesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="efb5e-135">En el panel de resultados, seleccione **FreshDesk** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="efb5e-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="efb5e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="efb5e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FreshDesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="efb5e-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="efb5e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de FreshDesk para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb5e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="efb5e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="efb5e-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="efb5e-142">Para configurar y probar el inicio de sesión único de Azure AD con FreshDesk, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="efb5e-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="efb5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="efb5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="efb5e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efb5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="efb5e-145">**[Creación de un usuario de prueba de FreshDesk](#creating-a-freshdesk-test-user)**: para tener un homólogo de Britta Simon en FreshDesk que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb5e-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="efb5e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efb5e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="efb5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="efb5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="efb5e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="efb5e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="efb5e-150">**Para configurar el inicio de sesión único de Azure AD con FreshDesk, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="efb5e-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="efb5e-151">En el Portal de administración de Azure, en la página de integración de la aplicación **FreshDesk**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="efb5e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="efb5e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="efb5e-155">En la sección **Dominio y direcciones URL de FreshDesk**, escriba la **dirección URL de inicio de sesión** como: `https://<tenant-name>.freshdesk.com` o cualquier otro valor que le sugiera Freshdesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="efb5e-157">Tenga en cuenta que este no es el valor real.</span><span class="sxs-lookup"><span data-stu-id="efb5e-157">Please note that this is not the real value.</span></span> <span data-ttu-id="efb5e-158">Tiene que actualizar este valor con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="efb5e-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="efb5e-159">Póngase en contacto con el [equipo de soporte técnico de FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="efb5e-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="efb5e-160">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="efb5e-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="efb5e-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="efb5e-162">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="efb5e-164">En la sección **Configuración de FreshDesk**, haga clic en **Configurar FreshDesk** para abrir la ventana Configurar inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="efb5e-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="efb5e-165">Copie la dirección URL del servicio de inicio de sesión único de SAML y la URL de cierre de sesión de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="efb5e-167">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Freshdesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="efb5e-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="efb5e-168">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="efb5e-169">![Administración](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="efb5e-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="efb5e-170">En la pestaña **Configuración general**, haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="efb5e-171">![Seguridad](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="efb5e-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="efb5e-172">En la sección **Seguridad** , realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="efb5e-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="efb5e-173">![Inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="efb5e-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="efb5e-174">a.</span><span class="sxs-lookup"><span data-stu-id="efb5e-174">a.</span></span> <span data-ttu-id="efb5e-175">En **Inicio de sesión único (SSO)**, seleccione **Activado**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="efb5e-176">b.</span><span class="sxs-lookup"><span data-stu-id="efb5e-176">b.</span></span> <span data-ttu-id="efb5e-177">Seleccione **Inicio de sesión único de SAML**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="efb5e-178">c.</span><span class="sxs-lookup"><span data-stu-id="efb5e-178">c.</span></span> <span data-ttu-id="efb5e-179">Escriba la **Dirección URL de inicio de sesión único de SAML** que copió desde Azure Portal en el cuadro de texto **URL de inicio de sesión SAML**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="efb5e-180">d.</span><span class="sxs-lookup"><span data-stu-id="efb5e-180">d.</span></span> <span data-ttu-id="efb5e-181">Escriba la **Dirección URL de cierre de sesión**  que copió desde Azure Portal en el cuadro de texto **URL de cierre de sesión**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="efb5e-182">e.</span><span class="sxs-lookup"><span data-stu-id="efb5e-182">e.</span></span> <span data-ttu-id="efb5e-183">Copie el valor de **Huella digital** desde el certificado descargado de Azure Portal y péguelo en el cuadro de texto **Huella digital del certificado de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="efb5e-184">Para obtener más información, consulte [Recuperación del valor de huella digital de un certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="efb5e-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="efb5e-185">f.</span><span class="sxs-lookup"><span data-stu-id="efb5e-185">f.</span></span> <span data-ttu-id="efb5e-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="efb5e-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb5e-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="efb5e-188">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efb5e-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="efb5e-190">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="efb5e-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="efb5e-191">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="efb5e-193">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="efb5e-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="efb5e-195">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="efb5e-197">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="efb5e-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="efb5e-199">a.</span><span class="sxs-lookup"><span data-stu-id="efb5e-199">a.</span></span> <span data-ttu-id="efb5e-200">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="efb5e-201">b.</span><span class="sxs-lookup"><span data-stu-id="efb5e-201">b.</span></span> <span data-ttu-id="efb5e-202">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efb5e-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="efb5e-203">c.</span><span class="sxs-lookup"><span data-stu-id="efb5e-203">c.</span></span> <span data-ttu-id="efb5e-204">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="efb5e-205">d.</span><span class="sxs-lookup"><span data-stu-id="efb5e-205">d.</span></span> <span data-ttu-id="efb5e-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="efb5e-207">Creación de un usuario de prueba de FreshDesk</span><span class="sxs-lookup"><span data-stu-id="efb5e-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="efb5e-208">Para permitir que los usuarios de Azure AD inicien sesión en FreshDesk, deben aprovisionarse en FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="efb5e-209">En el caso de FreshDesk, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="efb5e-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="efb5e-210">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="efb5e-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="efb5e-211">Inicie sesión en su inquilino de **Freshdesk** .</span><span class="sxs-lookup"><span data-stu-id="efb5e-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="efb5e-212">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="efb5e-213">![Administración](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="efb5e-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="efb5e-214">En la pestaña **Configuración general**, haga clic en **Agentes**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="efb5e-215">![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agentes")</span><span class="sxs-lookup"><span data-stu-id="efb5e-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="efb5e-216">Haga clic en **Nuevo agente**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="efb5e-217">![Nuevo agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Nuevo agente")</span><span class="sxs-lookup"><span data-stu-id="efb5e-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="efb5e-218">En el cuadro de diálogo Agent Information (Información de agente), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="efb5e-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="efb5e-219">![Información sobre agentes](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Información sobre agentes")</span><span class="sxs-lookup"><span data-stu-id="efb5e-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="efb5e-220">a.</span><span class="sxs-lookup"><span data-stu-id="efb5e-220">a.</span></span> <span data-ttu-id="efb5e-221">En el cuadro de texto **Nombre completo** , escriba el nombre de la cuenta de Azure AD que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="efb5e-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="efb5e-222">b.</span><span class="sxs-lookup"><span data-stu-id="efb5e-222">b.</span></span> <span data-ttu-id="efb5e-223">En el cuadro de texto **Email** (Correo electrónico), escriba la dirección de correo electrónico de la cuenta de Azure AD que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="efb5e-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="efb5e-224">c.</span><span class="sxs-lookup"><span data-stu-id="efb5e-224">c.</span></span> <span data-ttu-id="efb5e-225">En el cuadro de texto **Título** , escriba el título de la cuenta de Azure AD que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="efb5e-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="efb5e-226">d.</span><span class="sxs-lookup"><span data-stu-id="efb5e-226">d.</span></span> <span data-ttu-id="efb5e-227">Seleccione **Agents role** (Rol de agentes) y luego haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="efb5e-228">e.</span><span class="sxs-lookup"><span data-stu-id="efb5e-228">e.</span></span> <span data-ttu-id="efb5e-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="efb5e-230">El titular de la cuenta de Azure AD recibirá un mensaje de correo electrónico que incluye un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="efb5e-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="efb5e-231">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Freshdesk que proporcione Freshdesk para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="efb5e-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="efb5e-232">a FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="efb5e-233">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="efb5e-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="efb5e-234">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="efb5e-236">**Para asignar Britta Simon a FreshDesk, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="efb5e-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="efb5e-237">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="efb5e-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="efb5e-239">En la lista de aplicaciones, seleccione **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-239">In the applications list, select **FreshDesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="efb5e-241">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="efb5e-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-243">Click **Add** button.</span></span> <span data-ttu-id="efb5e-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="efb5e-246">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="efb5e-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="efb5e-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="efb5e-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="efb5e-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="efb5e-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="efb5e-249">Testing single sign-on</span></span>

<span data-ttu-id="efb5e-250">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="efb5e-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="efb5e-251">Al hacer clic en el icono de FreshDesk en el panel de acceso, debería obtener la página de inicio de sesión e iniciar sesión automáticamente en su aplicación FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="efb5e-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efb5e-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="efb5e-252">Additional resources</span></span>

* [<span data-ttu-id="efb5e-253">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efb5e-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efb5e-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="efb5e-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

