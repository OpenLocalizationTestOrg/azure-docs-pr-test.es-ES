---
title: "Tutorial: Integración de Azure Active Directory con Skydesk Email | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Skydesk Email."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 0ffcca4161fc836192fc9c9871a905f36ea76b32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="98d7d-103">Tutorial: Integración de Azure Active Directory con Skydesk Email</span><span class="sxs-lookup"><span data-stu-id="98d7d-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="98d7d-104">En este tutorial, aprenderá a integrar SkyDesk Email con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98d7d-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98d7d-105">Integrar Skydesk Email con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="98d7d-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="98d7d-106">Puede controlar en Azure AD quién tiene acceso a Skydesk Email.</span><span class="sxs-lookup"><span data-stu-id="98d7d-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="98d7d-107">Puede permitir que los usuarios inicien sesión automáticamente en Skydesk Email (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98d7d-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98d7d-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="98d7d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="98d7d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="98d7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98d7d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="98d7d-110">Prerequisites</span></span>

<span data-ttu-id="98d7d-111">Para configurar la integración de Azure AD con Skydesk Email, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="98d7d-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="98d7d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98d7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98d7d-113">Una suscripción habilitada para el inicio de sesión único en Skydesk Email</span><span class="sxs-lookup"><span data-stu-id="98d7d-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98d7d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="98d7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98d7d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="98d7d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98d7d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="98d7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98d7d-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes [oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98d7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98d7d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="98d7d-118">Scenario description</span></span>
<span data-ttu-id="98d7d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="98d7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98d7d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="98d7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98d7d-121">Adición de Skydesk Email desde la galería</span><span class="sxs-lookup"><span data-stu-id="98d7d-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="98d7d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98d7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="98d7d-123">Adición de Skydesk Email desde la galería</span><span class="sxs-lookup"><span data-stu-id="98d7d-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="98d7d-124">Para configurar la integración de Skydesk Email en Azure AD, será preciso que agregue Skydesk Email desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="98d7d-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="98d7d-125">**Para agregar Skydesk Email desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="98d7d-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="98d7d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="98d7d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="98d7d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="98d7d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98d7d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="98d7d-133">En el cuadro Buscar, escriba **Skydesk Email**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-133">In the search box, type **SkyDesk Email**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="98d7d-135">En el panel de resultados, seleccione **SkyDesk Email** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98d7d-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98d7d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98d7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98d7d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SkyDesk Email utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="98d7d-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="98d7d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Skydesk Email para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98d7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="98d7d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Skydesk Email.</span><span class="sxs-lookup"><span data-stu-id="98d7d-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="98d7d-141">Para establecer la relación de vínculo, en SkyDesk Email, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="98d7d-142">Para configurar y probar el inicio de sesión único de Azure AD con Skydesk Email, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="98d7d-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="98d7d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="98d7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="98d7d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98d7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98d7d-145">**[Creación de un usuario de prueba de Skydesk Email](#creating-a-skydesk-email-test-user)**: para tener un homólogo de Britta Simon en Skydesk Email que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98d7d-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="98d7d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98d7d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98d7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="98d7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98d7d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98d7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98d7d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="98d7d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="98d7d-150">**Para configurar el inicio de sesión único de Azure AD con Skydesk Email, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="98d7d-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="98d7d-151">En Azure Portal, en la página de integración de la aplicación **SkyDesk Email**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="98d7d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="98d7d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="98d7d-155">En la sección **Dominio y direcciones URL de SkyDesk Email**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="98d7d-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="98d7d-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://mail.skydesk.jp/portal/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="98d7d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98d7d-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="98d7d-158">The value is not real.</span></span> <span data-ttu-id="98d7d-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="98d7d-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="98d7d-160">Póngase en contacto con el [equipo de soporte técnico de SkyDesk Email](https://www.skydesk.sg/support/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="98d7d-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
4. <span data-ttu-id="98d7d-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="98d7d-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="98d7d-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="98d7d-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="98d7d-165">En la sección **Configuración de SkyDesk Email**, haga clic en **Configurar SkyDesk Email** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="98d7d-166">Copie los valores **Sign-Out URL y SAML Single Sign-On Service URL** (Dirección URL de cierre de sesión y Dirección URL del servicio de inicio de sesión único de SAML) de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="98d7d-168">Para habilitar SSO en **Skydesk Email**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98d7d-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="98d7d-169">a.</span><span class="sxs-lookup"><span data-stu-id="98d7d-169">a.</span></span> <span data-ttu-id="98d7d-170">Inicie sesión en su cuenta de correo de Skydesk Email como administrador.</span><span class="sxs-lookup"><span data-stu-id="98d7d-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="98d7d-171">b.</span><span class="sxs-lookup"><span data-stu-id="98d7d-171">b.</span></span> <span data-ttu-id="98d7d-172">En el menú en la parte superior, haga clic en **Setup** (Configurar) y seleccione **Org** (Organización).</span><span class="sxs-lookup"><span data-stu-id="98d7d-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="98d7d-174">c.</span><span class="sxs-lookup"><span data-stu-id="98d7d-174">c.</span></span> <span data-ttu-id="98d7d-175">En el panel izquierdo, haga clic en **Domains** (Dominios).</span><span class="sxs-lookup"><span data-stu-id="98d7d-175">Click on **Domains** from the left panel.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="98d7d-177">d.</span><span class="sxs-lookup"><span data-stu-id="98d7d-177">d.</span></span> <span data-ttu-id="98d7d-178">Haga clic en **Add Domain** (Agregar dominio).</span><span class="sxs-lookup"><span data-stu-id="98d7d-178">Click on **Add Domain**.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="98d7d-180">e.</span><span class="sxs-lookup"><span data-stu-id="98d7d-180">e.</span></span> <span data-ttu-id="98d7d-181">Escriba el nombre de dominio y, a continuación, compruebe el dominio.</span><span class="sxs-lookup"><span data-stu-id="98d7d-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="98d7d-183">f.</span><span class="sxs-lookup"><span data-stu-id="98d7d-183">f.</span></span> <span data-ttu-id="98d7d-184">Haga clic en **SAML Authentication** (Autenticación SAML) desde el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="98d7d-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="98d7d-186">En la página de diálogo **SAML Authentication** (Autenticación SAML), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98d7d-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="98d7d-188">Para usar la autenticación basada en SAML, necesita **comprobar el dominio** o configurar la **dirección URL del portal**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="98d7d-189">Puede configurar la dirección URL del portal con el nombre único.</span><span class="sxs-lookup"><span data-stu-id="98d7d-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="98d7d-191">a.</span><span class="sxs-lookup"><span data-stu-id="98d7d-191">a.</span></span> <span data-ttu-id="98d7d-192">En el cuadro de texto **Login URL** (Dirección URL de inicio de sesión), pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL de inicio de sesión único de SAML) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="98d7d-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="98d7d-193">b.</span><span class="sxs-lookup"><span data-stu-id="98d7d-193">b.</span></span> <span data-ttu-id="98d7d-194">En el cuadro de texto **Logout** (Dirección URL de cierre de sesión), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="98d7d-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="98d7d-195">c.</span><span class="sxs-lookup"><span data-stu-id="98d7d-195">c.</span></span> <span data-ttu-id="98d7d-196">**Cambiar dirección URL de contraseña** es opcional, déjelo en blanco.</span><span class="sxs-lookup"><span data-stu-id="98d7d-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="98d7d-197">d.</span><span class="sxs-lookup"><span data-stu-id="98d7d-197">d.</span></span> <span data-ttu-id="98d7d-198">Haga clic en **Get Key From File** (Obtener clave de archivo) para seleccionar el certificado descargado desde Azure Portal y, después, haga clic en **Abrir** para cargar el certificado.</span><span class="sxs-lookup"><span data-stu-id="98d7d-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="98d7d-199">e.</span><span class="sxs-lookup"><span data-stu-id="98d7d-199">e.</span></span> <span data-ttu-id="98d7d-200">En **Algoritmo**, seleccione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="98d7d-201">f.</span><span class="sxs-lookup"><span data-stu-id="98d7d-201">f.</span></span> <span data-ttu-id="98d7d-202">Haga clic en **Aceptar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="98d7d-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="98d7d-203">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98d7d-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="98d7d-204">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="98d7d-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="98d7d-205">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="98d7d-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98d7d-206">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98d7d-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="98d7d-207">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="98d7d-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="98d7d-209">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="98d7d-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="98d7d-210">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98d7d-212">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98d7d-214">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98d7d-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98d7d-216">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="98d7d-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98d7d-218">a.</span><span class="sxs-lookup"><span data-stu-id="98d7d-218">a.</span></span> <span data-ttu-id="98d7d-219">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98d7d-220">b.</span><span class="sxs-lookup"><span data-stu-id="98d7d-220">b.</span></span> <span data-ttu-id="98d7d-221">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98d7d-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98d7d-222">c.</span><span class="sxs-lookup"><span data-stu-id="98d7d-222">c.</span></span> <span data-ttu-id="98d7d-223">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="98d7d-224">d.</span><span class="sxs-lookup"><span data-stu-id="98d7d-224">d.</span></span> <span data-ttu-id="98d7d-225">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="98d7d-226">Creación de un usuario de prueba de Skydesk Email</span><span class="sxs-lookup"><span data-stu-id="98d7d-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="98d7d-227">En esta sección, creará un usuario llamado Britta Simon en Skydesk Email.</span><span class="sxs-lookup"><span data-stu-id="98d7d-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="98d7d-228">Haga clic en **User Access** (Acceso de usuario) en el panel de la izquierda de Skydesk Email y, a continuación, escriba su nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="98d7d-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="98d7d-230">Si necesita crear usuarios de forma masiva, debe ponerse en contacto con el [equipo de soporte al cliente de Skydesk Email](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="98d7d-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="98d7d-231">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98d7d-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="98d7d-232">En esta sección, concederá acceso a Britta Simon a SkyDesk Email para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="98d7d-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="98d7d-234">**Para asignar a Britta Simon a Skydesk Email, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="98d7d-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="98d7d-235">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="98d7d-237">En la lista de aplicaciones, seleccione **Skydesk Email**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="98d7d-239">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="98d7d-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-241">Click **Add** button.</span></span> <span data-ttu-id="98d7d-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="98d7d-244">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="98d7d-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="98d7d-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98d7d-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="98d7d-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98d7d-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="98d7d-247">Testing single sign-on</span></span>

<span data-ttu-id="98d7d-248">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="98d7d-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="98d7d-249">Al hacer clic en el icono de Skydesk Email en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Skydesk Email.</span><span class="sxs-lookup"><span data-stu-id="98d7d-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98d7d-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="98d7d-250">Additional resources</span></span>

* [<span data-ttu-id="98d7d-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98d7d-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98d7d-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="98d7d-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

