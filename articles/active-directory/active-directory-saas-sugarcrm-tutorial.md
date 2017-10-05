---
title: "Tutorial: Integración de Azure Active Directory con Sugar CRM | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c27aef24e859522b8001ecb747906abdca14d87a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="c7973-103">Tutorial: Integración de Azure Active Directory con Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="c7973-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="c7973-104">En este tutorial, aprenderá cómo integrar Sugar CRM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7973-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7973-105">La integración de Sugar CRM con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c7973-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7973-106">Puede controlar en Azure AD quién tiene acceso a Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="c7973-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="c7973-107">Puede permitir que los usuarios inicien sesión automáticamente en Sugar CRM (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7973-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c7973-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7973-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7973-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7973-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c7973-110">Prerequisites</span></span>

<span data-ttu-id="c7973-111">Para configurar la integración de Azure AD con Sugar CRM, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c7973-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="c7973-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7973-113">Un suscripción habilitada para el inicio de sesión único en SugarCRM</span><span class="sxs-lookup"><span data-stu-id="c7973-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7973-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c7973-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7973-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c7973-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7973-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c7973-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7973-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7973-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7973-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c7973-118">Scenario description</span></span>
<span data-ttu-id="c7973-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c7973-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7973-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c7973-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7973-121">Agregación de Sugar CRM desde la galería</span><span class="sxs-lookup"><span data-stu-id="c7973-121">Adding Sugar CRM from the gallery</span></span>
2. <span data-ttu-id="c7973-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="c7973-123">Agregación de Sugar CRM desde la galería</span><span class="sxs-lookup"><span data-stu-id="c7973-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="c7973-124">Para configurar la integración de Sugar CRM en Azure AD, deberá agregar Sugar CRM desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c7973-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7973-125">**Para agregar Sugar CRM desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c7973-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7973-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7973-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7973-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c7973-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7973-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c7973-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c7973-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7973-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c7973-133">En el cuadro de búsqueda, escriba **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="c7973-133">In the search box, type **Sugar CRM**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="c7973-135">En el panel de resultados, seleccione **Sugar CRM** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7973-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7973-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7973-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sugar CRM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c7973-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7973-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Sugar CRM para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7973-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="c7973-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="c7973-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="c7973-141">Para establecer la relación de vínculo, en Sugar CRM, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c7973-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c7973-142">Para configurar y probar el inicio de sesión único de Azure AD con Sugar CRM, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c7973-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7973-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c7973-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7973-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7973-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7973-145">**[Creación de un usuario de prueba de Sugar CRM](#creating-a-sugar-crm-test-user)**: para tener un homólogo de Britta Simon en Sugar CRM que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7973-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7973-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7973-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7973-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c7973-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7973-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7973-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="c7973-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="c7973-150">**Para configurar el inicio de sesión único de Azure AD con Sugar CRM, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c7973-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="c7973-151">En Azure Portal, en la página de integración de la aplicación **Sugar CRM**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c7973-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c7973-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c7973-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="c7973-155">En la sección **Dominio y direcciones URL de Sugar CRM**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7973-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="c7973-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c7973-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="c7973-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="c7973-158">The value is not real.</span></span> <span data-ttu-id="c7973-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="c7973-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="c7973-160">Póngase en contacto con el [equipo de soporte técnico de Sugar CRM](https://support.sugarcrm.com/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="c7973-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="c7973-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7973-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="c7973-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c7973-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7973-165">En la sección **Configuración de Sugar CRM**, haga clic en **Configurar Sugar CRM** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="c7973-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c7973-166">Copie la **dirección URL de cierre de sesión y la dirección URL del servicio de inicio de sesión único de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="c7973-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="c7973-168">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de SugarCRM como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7973-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="c7973-169">Vaya a **Administración**.</span><span class="sxs-lookup"><span data-stu-id="c7973-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="c7973-170">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="c7973-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="c7973-171">En la sección **Administración**, haga clic en **Administración de contraseñas**.</span><span class="sxs-lookup"><span data-stu-id="c7973-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="c7973-172">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="c7973-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="c7973-173">Seleccione **Habilitar autenticación SAML**.</span><span class="sxs-lookup"><span data-stu-id="c7973-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="c7973-174">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="c7973-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="c7973-175">En la sección **Autenticación SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7973-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c7973-176">![Autenticación SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="c7973-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="c7973-177">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-177">a.</span></span> <span data-ttu-id="c7973-178">En el cuadro de texto **Login URL** (Dirección URL de inicio de sesión), pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL de inicio de sesión único de SAML) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c7973-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="c7973-179">b.</span><span class="sxs-lookup"><span data-stu-id="c7973-179">b.</span></span> <span data-ttu-id="c7973-180">En el cuadro de texto **SLO URL** (Dirección URL de SLO), pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c7973-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="c7973-181">c.</span><span class="sxs-lookup"><span data-stu-id="c7973-181">c.</span></span> <span data-ttu-id="c7973-182">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego pegue todo el certificado en el cuadro de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="c7973-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="c7973-183">d.</span><span class="sxs-lookup"><span data-stu-id="c7973-183">d.</span></span> <span data-ttu-id="c7973-184">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c7973-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c7973-185">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7973-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7973-186">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c7973-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7973-187">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7973-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7973-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7973-189">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c7973-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c7973-191">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c7973-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7973-192">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7973-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7973-194">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c7973-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7973-196">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7973-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7973-198">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c7973-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7973-200">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-200">a.</span></span> <span data-ttu-id="c7973-201">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7973-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7973-202">b.</span><span class="sxs-lookup"><span data-stu-id="c7973-202">b.</span></span> <span data-ttu-id="c7973-203">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7973-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7973-204">c.</span><span class="sxs-lookup"><span data-stu-id="c7973-204">c.</span></span> <span data-ttu-id="c7973-205">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c7973-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7973-206">d.</span><span class="sxs-lookup"><span data-stu-id="c7973-206">d.</span></span> <span data-ttu-id="c7973-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c7973-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="c7973-208">Creación de un usuario de prueba de Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="c7973-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="c7973-209">Para permitir que los usuarios de Azure AD inicien sesión en SugarCRM, deben aprovisionarse en SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="c7973-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="c7973-210">En el caso de SugarCRM, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="c7973-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="c7973-211">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c7973-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c7973-212">Inicie sesión en su sitio de compañía de **SugarCRM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7973-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="c7973-213">Vaya a **Administración**.</span><span class="sxs-lookup"><span data-stu-id="c7973-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="c7973-214">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="c7973-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="c7973-215">En la sección **Administración**, haga clic en **Administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c7973-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="c7973-216">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="c7973-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="c7973-217">Vaya a **Usuarios \> Crear nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="c7973-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="c7973-218">![Creación de nuevos usuarios](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Creación de nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="c7973-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="c7973-219">En la pestaña **Perfil de usuario** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c7973-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="c7973-220">![Nuevo usuario](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="c7973-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="c7973-221">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-221">a.</span></span> <span data-ttu-id="c7973-222">Escriba el **nombre de usuario**, **apellidos** y la **dirección de correo electrónico** de un usuario de Azure Active Directory válido en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="c7973-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
6. <span data-ttu-id="c7973-223">Como **Estado**, seleccione **Activo**.</span><span class="sxs-lookup"><span data-stu-id="c7973-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="c7973-224">En la pestaña Contraseña, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7973-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="c7973-225">![Nuevo usuario](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="c7973-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="c7973-226">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-226">a.</span></span> <span data-ttu-id="c7973-227">Escriba la contraseña en el cuadro de texto relacionado.</span><span class="sxs-lookup"><span data-stu-id="c7973-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="c7973-228">b.</span><span class="sxs-lookup"><span data-stu-id="c7973-228">b.</span></span> <span data-ttu-id="c7973-229">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="c7973-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c7973-230">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de SugarCRM ofrecida por SugarCRM para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="c7973-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7973-231">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7973-232">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="c7973-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c7973-234">**Para asignar a Britta Simon a Sugar CRM, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c7973-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="c7973-235">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c7973-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c7973-237">En la lista de aplicaciones, seleccione **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="c7973-237">In the applications list, select **Sugar CRM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="c7973-239">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7973-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c7973-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c7973-241">Click **Add** button.</span></span> <span data-ttu-id="c7973-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c7973-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c7973-244">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c7973-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7973-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7973-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7973-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c7973-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7973-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c7973-247">Testing single sign-on</span></span>

<span data-ttu-id="c7973-248">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c7973-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7973-249">Al hacer clic en el icono de Sugar CRM en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="c7973-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7973-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c7973-250">Additional resources</span></span>

* [<span data-ttu-id="c7973-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7973-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7973-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7973-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

