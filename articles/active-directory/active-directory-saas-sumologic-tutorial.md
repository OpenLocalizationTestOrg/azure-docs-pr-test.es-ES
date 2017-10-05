---
title: "Tutorial: Integración de Azure Active Directory con SumoLogic | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="de0c9-103">Tutorial: Integración de Azure Active Directory con SumoLogic</span><span class="sxs-lookup"><span data-stu-id="de0c9-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="de0c9-104">En este tutorial, aprenderá cómo integrar SumoLogic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de0c9-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de0c9-105">La integración de SumoLogic con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="de0c9-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="de0c9-106">Puede controlar en Azure AD quién tiene acceso a SumoLogic</span><span class="sxs-lookup"><span data-stu-id="de0c9-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="de0c9-107">Puede permitir que los usuarios inicien sesión automáticamente en SumoLogic (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de0c9-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de0c9-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="de0c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="de0c9-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de0c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de0c9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="de0c9-110">Prerequisites</span></span>

<span data-ttu-id="de0c9-111">Para configurar la integración de Azure AD con SumoLogic, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="de0c9-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="de0c9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de0c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de0c9-113">Una suscripción habilitada para el inicio de sesión único en SumoLogic</span><span class="sxs-lookup"><span data-stu-id="de0c9-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de0c9-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="de0c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de0c9-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="de0c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de0c9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="de0c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de0c9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de0c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de0c9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="de0c9-118">Scenario description</span></span>
<span data-ttu-id="de0c9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="de0c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de0c9-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="de0c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de0c9-121">Agregación de SumoLogic desde la galería</span><span class="sxs-lookup"><span data-stu-id="de0c9-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="de0c9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de0c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="de0c9-123">Agregación de SumoLogic desde la galería</span><span class="sxs-lookup"><span data-stu-id="de0c9-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="de0c9-124">Para configurar la integración de SumoLogic en Azure AD, deberá agregar SumoLogic desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="de0c9-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="de0c9-125">**Para agregar SumoLogic desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="de0c9-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="de0c9-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de0c9-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="de0c9-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="de0c9-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="de0c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="de0c9-133">En el cuadro de búsqueda, escriba **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-133">In the search box, type **SumoLogic**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="de0c9-135">En el panel de resultados, seleccione **SumoLogic** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="de0c9-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de0c9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de0c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de0c9-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SumoLogic con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="de0c9-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de0c9-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SumoLogic para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de0c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="de0c9-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="de0c9-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="de0c9-141">Para establecer la relación de vínculo, en SumoLogic, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="de0c9-142">Para configurar y probar el inicio de sesión único de Azure AD con SumoLogic, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="de0c9-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="de0c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="de0c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="de0c9-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de0c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de0c9-145">**[Creación de un usuario de prueba para SumoLogic](#creating-a-sumologic-test-user)**: para tener un homólogo de Britta Simon en SumoLogic que esté vinculado a la representación de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de0c9-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="de0c9-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de0c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de0c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="de0c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de0c9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de0c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de0c9-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="de0c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="de0c9-150">**Para configurar el inicio de sesión único de Azure AD con SumoLogic, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="de0c9-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="de0c9-151">En Azure Portal, en la página de integración de la aplicación **SumoLogic**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="de0c9-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="de0c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="de0c9-155">En la sección **Dominio y direcciones URL de SumoLogic**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="de0c9-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="de0c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="de0c9-157">a.</span></span> <span data-ttu-id="de0c9-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.SumoLogic.com`.</span><span class="sxs-lookup"><span data-stu-id="de0c9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="de0c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="de0c9-159">b.</span></span> <span data-ttu-id="de0c9-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="de0c9-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="de0c9-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="de0c9-161">These values are not real.</span></span> <span data-ttu-id="de0c9-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="de0c9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="de0c9-163">Póngase en contacto con el [equipo de soporte al cliente de SumoLogic](https://www.sumologic.com/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="de0c9-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="de0c9-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="de0c9-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="de0c9-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="de0c9-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de0c9-168">En la sección **Configuración de SumoLogic**, haga clic en **Configurar SumoLogic** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="de0c9-169">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="de0c9-171">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de SumoLogic como administrador.</span><span class="sxs-lookup"><span data-stu-id="de0c9-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="de0c9-172">Vaya a **Administrar \> Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="de0c9-173">![Administración](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="de0c9-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="de0c9-174">Haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="de0c9-175">![Configuración de seguridad global](./media/active-directory-saas-sumologic-tutorial/ic778557.png "configuración de seguridad global")</span><span class="sxs-lookup"><span data-stu-id="de0c9-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="de0c9-176">En la lista **Seleccionar una configuración o crear una nueva**, seleccione **Azure AD** y, después, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="de0c9-177">![Configuración de SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configuración de SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="de0c9-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="de0c9-178">En el cuadro de diálogo **Configurar SAML 2.0** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="de0c9-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="de0c9-179">![Configuración de SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configuración de SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="de0c9-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="de0c9-180">a.</span><span class="sxs-lookup"><span data-stu-id="de0c9-180">a.</span></span> <span data-ttu-id="de0c9-181">En el cuadro de texto **Nombre de configuración**, escriba **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="de0c9-182">b.</span><span class="sxs-lookup"><span data-stu-id="de0c9-182">b.</span></span> <span data-ttu-id="de0c9-183">Seleccione **Modo de depuración**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="de0c9-184">c.</span><span class="sxs-lookup"><span data-stu-id="de0c9-184">c.</span></span> <span data-ttu-id="de0c9-185">En el cuadro de texto **Issuer** (Emisor), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="de0c9-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="de0c9-186">d.</span><span class="sxs-lookup"><span data-stu-id="de0c9-186">d.</span></span> <span data-ttu-id="de0c9-187">En el cuadro de texto **Authn Request URL** (Dirección URL de solicitud de autenticación), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="de0c9-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="de0c9-188">e.</span><span class="sxs-lookup"><span data-stu-id="de0c9-188">e.</span></span> <span data-ttu-id="de0c9-189">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego pegue todo el certificado en el cuadro de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="de0c9-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="de0c9-190">f.</span><span class="sxs-lookup"><span data-stu-id="de0c9-190">f.</span></span> <span data-ttu-id="de0c9-191">Como **Atributo de correo electrónico**, seleccione **Usar SAML Subject**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="de0c9-192">g.</span><span class="sxs-lookup"><span data-stu-id="de0c9-192">g.</span></span> <span data-ttu-id="de0c9-193">Seleccione **Configuración de inicio de sesión iniciada por el SP**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="de0c9-194">h.</span><span class="sxs-lookup"><span data-stu-id="de0c9-194">h.</span></span> <span data-ttu-id="de0c9-195">En el cuadro de texto de la **ruta de acceso de inicio de sesión**, escriba **Azure** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="de0c9-196">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="de0c9-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="de0c9-197">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="de0c9-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="de0c9-198">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de0c9-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de0c9-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de0c9-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="de0c9-200">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="de0c9-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="de0c9-202">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="de0c9-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="de0c9-203">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de0c9-205">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de0c9-207">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="de0c9-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de0c9-209">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="de0c9-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de0c9-211">a.</span><span class="sxs-lookup"><span data-stu-id="de0c9-211">a.</span></span> <span data-ttu-id="de0c9-212">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de0c9-213">b.</span><span class="sxs-lookup"><span data-stu-id="de0c9-213">b.</span></span> <span data-ttu-id="de0c9-214">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de0c9-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de0c9-215">c.</span><span class="sxs-lookup"><span data-stu-id="de0c9-215">c.</span></span> <span data-ttu-id="de0c9-216">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="de0c9-217">d.</span><span class="sxs-lookup"><span data-stu-id="de0c9-217">d.</span></span> <span data-ttu-id="de0c9-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="de0c9-219">Creación de un usuario de prueba de SumoLogic</span><span class="sxs-lookup"><span data-stu-id="de0c9-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="de0c9-220">Para permitir que los usuarios de Azure AD inicien sesión en SumoLogic, deben aprovisionarse a SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="de0c9-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="de0c9-221">En el caso de SumoLogic, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="de0c9-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="de0c9-222">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="de0c9-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="de0c9-223">Inicie sesión en su inquilino de **SumoLogic** .</span><span class="sxs-lookup"><span data-stu-id="de0c9-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="de0c9-224">Vaya a **Administrar \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="de0c9-225">![Usuarios](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="de0c9-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="de0c9-226">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-226">Click **Add**.</span></span>
   
    <span data-ttu-id="de0c9-227">![Usuarios](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="de0c9-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="de0c9-228">En el cuadro de diálogo **Nuevo usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="de0c9-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="de0c9-229">![Nuevo usuario](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="de0c9-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="de0c9-230">a.</span><span class="sxs-lookup"><span data-stu-id="de0c9-230">a.</span></span> <span data-ttu-id="de0c9-231">Escriba la información relacionada de la cuenta de Azure AD que quiere aprovisionar en los cuadros de texto **First Name** (Nombre), **Last Name** (Apellidos) y **Email** (Correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="de0c9-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="de0c9-232">b.</span><span class="sxs-lookup"><span data-stu-id="de0c9-232">b.</span></span> <span data-ttu-id="de0c9-233">Seleccione un rol.</span><span class="sxs-lookup"><span data-stu-id="de0c9-233">Select a role.</span></span>
  
    <span data-ttu-id="de0c9-234">c.</span><span class="sxs-lookup"><span data-stu-id="de0c9-234">c.</span></span> <span data-ttu-id="de0c9-235">Como **Estado**, seleccione **Activo**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="de0c9-236">d.</span><span class="sxs-lookup"><span data-stu-id="de0c9-236">d.</span></span> <span data-ttu-id="de0c9-237">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="de0c9-238">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de SumoLogic ofrecida por SumoLogic para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="de0c9-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="de0c9-239">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de0c9-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="de0c9-240">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="de0c9-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="de0c9-242">**Para asignar a Britta Simon a SumoLogic, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="de0c9-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="de0c9-243">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="de0c9-245">En la lista de aplicaciones, seleccione **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-245">In the applications list, select **SumoLogic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="de0c9-247">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="de0c9-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-249">Click **Add** button.</span></span> <span data-ttu-id="de0c9-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="de0c9-252">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="de0c9-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="de0c9-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de0c9-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="de0c9-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de0c9-255">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="de0c9-255">Testing single sign-on</span></span>

<span data-ttu-id="de0c9-256">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="de0c9-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="de0c9-257">Al hacer clic en el icono de SumoLogic en el panel de acceso, debería iniciar sesión automáticamente en la aplicación SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="de0c9-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de0c9-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="de0c9-258">Additional resources</span></span>

* [<span data-ttu-id="de0c9-259">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de0c9-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de0c9-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de0c9-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

