---
title: "Tutorial: integración de Azure Active Directory con Egnyte | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="83748-103">Tutorial: integración de Azure Active Directory con Egnyte</span><span class="sxs-lookup"><span data-stu-id="83748-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="83748-104">En este tutorial, aprenderá a integrar Egnyte con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83748-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83748-105">Integrar Egnyte con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="83748-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83748-106">Puede controlar en Azure AD quién tiene acceso a Egnyte.</span><span class="sxs-lookup"><span data-stu-id="83748-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="83748-107">Puede permitir que los usuarios inicien sesión automáticamente en Egnyte (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83748-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83748-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="83748-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="83748-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83748-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83748-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="83748-110">Prerequisites</span></span>

<span data-ttu-id="83748-111">Para configurar la integración de Azure AD con Egnyte, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="83748-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="83748-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83748-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83748-113">Una suscripción habilitada para el inicio de sesión único en Egnyte</span><span class="sxs-lookup"><span data-stu-id="83748-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83748-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="83748-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83748-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="83748-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83748-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="83748-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83748-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83748-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83748-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="83748-118">Scenario description</span></span>
<span data-ttu-id="83748-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="83748-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83748-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="83748-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83748-121">Adición de Egnyte desde la galería</span><span class="sxs-lookup"><span data-stu-id="83748-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="83748-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83748-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="83748-123">Adición de Egnyte desde la galería</span><span class="sxs-lookup"><span data-stu-id="83748-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="83748-124">Para configurar la integración de Egnyte en Azure AD, deberá agregar Egnyte desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="83748-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83748-125">**Para agregar Egnyte desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="83748-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83748-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83748-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83748-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="83748-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83748-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="83748-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="83748-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83748-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="83748-133">En el cuadro de búsqueda, escriba **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="83748-133">In the search box, type **Egnyte**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="83748-135">En el panel de resultados, seleccione **Egnyte** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83748-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83748-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83748-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83748-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Egnyte con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="83748-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83748-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Egnyte para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83748-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="83748-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Egnyte.</span><span class="sxs-lookup"><span data-stu-id="83748-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="83748-141">Para establecer la relación de vínculo, en Egnyte, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="83748-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83748-142">Para configurar y probar el inicio de sesión único de Azure AD con Egnyte, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="83748-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83748-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="83748-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83748-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83748-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83748-145">**[Creación de un usuario de prueba de Egnyte](#creating-an-egnyte-test-user)**: para tener un homólogo de Britta Simon en Egnyte que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83748-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="83748-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83748-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83748-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="83748-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83748-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83748-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83748-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Egnyte.</span><span class="sxs-lookup"><span data-stu-id="83748-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="83748-150">**Para configurar el inicio de sesión único de Azure AD con Egnyte, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="83748-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="83748-151">En Azure Portal, en la página de integración de la aplicación **Egnyte**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="83748-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="83748-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="83748-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="83748-155">En la sección **Dominio y direcciones URL de Egnyte**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="83748-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="83748-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.egnyte.com`.</span><span class="sxs-lookup"><span data-stu-id="83748-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83748-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="83748-158">This value is not real.</span></span> <span data-ttu-id="83748-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="83748-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="83748-160">Póngase en contacto con el [equipo de soporte técnico de Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="83748-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="83748-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="83748-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="83748-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="83748-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="83748-165">En la sección **Configuración de Egnyte**, haga clic en **Configurar Egnyte** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="83748-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="83748-166">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="83748-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="83748-168">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Egnyte como administrador.</span><span class="sxs-lookup"><span data-stu-id="83748-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="83748-169">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="83748-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="83748-170">![Configuración](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="83748-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="83748-171">En el menú, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="83748-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="83748-172">![Configuración](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="83748-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="83748-173">Haga clic en la pestaña **Configuración** y luego haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="83748-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="83748-174">![Seguridad](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="83748-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="83748-175">En la sección **Autenticación de inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="83748-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="83748-176">![Autenticación de inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Autenticación de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="83748-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="83748-177">a.</span><span class="sxs-lookup"><span data-stu-id="83748-177">a.</span></span> <span data-ttu-id="83748-178">En **Autenticación de inicio de sesión único**, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="83748-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="83748-179">b.</span><span class="sxs-lookup"><span data-stu-id="83748-179">b.</span></span> <span data-ttu-id="83748-180">En **Proveedor de identidades**, seleccione **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="83748-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="83748-181">c.</span><span class="sxs-lookup"><span data-stu-id="83748-181">c.</span></span> <span data-ttu-id="83748-182">Pegue el valor de **Dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal en el cuadro de texto **URL de inicio de sesión del proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="83748-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="83748-183">d.</span><span class="sxs-lookup"><span data-stu-id="83748-183">d.</span></span> <span data-ttu-id="83748-184">Pegue el valor del **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **Identity Provider Entity ID** (Id. de entidad del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="83748-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="83748-185">e.</span><span class="sxs-lookup"><span data-stu-id="83748-185">e.</span></span> <span data-ttu-id="83748-186">Abra el certificado codificado en base 64 descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="83748-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="83748-187">f.</span><span class="sxs-lookup"><span data-stu-id="83748-187">f.</span></span> <span data-ttu-id="83748-188">En **Asignación de usuario predeterminada**, seleccione **Dirección de correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="83748-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="83748-189">g.</span><span class="sxs-lookup"><span data-stu-id="83748-189">g.</span></span> <span data-ttu-id="83748-190">En **Usar valor de emisor específico del dominio**, seleccione **Deshabilitado**.</span><span class="sxs-lookup"><span data-stu-id="83748-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="83748-191">h.</span><span class="sxs-lookup"><span data-stu-id="83748-191">h.</span></span> <span data-ttu-id="83748-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="83748-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="83748-193">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83748-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="83748-194">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="83748-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="83748-195">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83748-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83748-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83748-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="83748-197">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="83748-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="83748-199">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="83748-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83748-200">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83748-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83748-202">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="83748-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83748-204">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83748-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83748-206">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="83748-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83748-208">a.</span><span class="sxs-lookup"><span data-stu-id="83748-208">a.</span></span> <span data-ttu-id="83748-209">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83748-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83748-210">b.</span><span class="sxs-lookup"><span data-stu-id="83748-210">b.</span></span> <span data-ttu-id="83748-211">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83748-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83748-212">c.</span><span class="sxs-lookup"><span data-stu-id="83748-212">c.</span></span> <span data-ttu-id="83748-213">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="83748-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="83748-214">d.</span><span class="sxs-lookup"><span data-stu-id="83748-214">d.</span></span> <span data-ttu-id="83748-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="83748-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="83748-216">Creación de un usuario de prueba de Egnyte</span><span class="sxs-lookup"><span data-stu-id="83748-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="83748-217">Para permitir que los usuarios de Azure AD inicien sesión en Egnyte, deben aprovisionarse en Egnyte.</span><span class="sxs-lookup"><span data-stu-id="83748-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="83748-218">En el caso de Egnyte, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="83748-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="83748-219">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="83748-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="83748-220">Inicie sesión en el sitio de la compañía de **Egnyte** como administrador.</span><span class="sxs-lookup"><span data-stu-id="83748-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="83748-221">Vaya a **Configuración \> Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="83748-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="83748-222">Haga clic en **Agregar nuevo usuario**y luego seleccione el tipo de usuario que quiera agregar.</span><span class="sxs-lookup"><span data-stu-id="83748-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="83748-223">![Usuarios](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="83748-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="83748-224">En la sección **Nuevo usuario estándar** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="83748-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="83748-225">![Nuevo usuario estándar](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Nuevo usuario estándar")</span><span class="sxs-lookup"><span data-stu-id="83748-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="83748-226">a.</span><span class="sxs-lookup"><span data-stu-id="83748-226">a.</span></span> <span data-ttu-id="83748-227">En los campos **Correo electrónico** y **Nombre de usuario**, escriba la información solicitada, y agregue los restantes datos de la cuenta válida de Azure Active Directory que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="83748-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="83748-228">b.</span><span class="sxs-lookup"><span data-stu-id="83748-228">b.</span></span> <span data-ttu-id="83748-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="83748-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="83748-230">El titular de la cuenta de Azure Active Directory recibirá una notificación por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="83748-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="83748-231">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Egnyte que proporcione Egnyte para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="83748-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="83748-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83748-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="83748-233">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Egnyte.</span><span class="sxs-lookup"><span data-stu-id="83748-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="83748-235">**Para asignar a Britta Simon a Egnyte, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="83748-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="83748-236">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="83748-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="83748-238">En la lista de aplicaciones, seleccione **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="83748-238">In the applications list, select **Egnyte**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="83748-240">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="83748-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="83748-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="83748-242">Click **Add** button.</span></span> <span data-ttu-id="83748-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="83748-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="83748-245">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="83748-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83748-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="83748-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83748-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="83748-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83748-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="83748-248">Testing single sign-on</span></span>

<span data-ttu-id="83748-249">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="83748-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="83748-250">Al hacer clic en el icono de Egnyte en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Egnyte.</span><span class="sxs-lookup"><span data-stu-id="83748-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="83748-251">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="83748-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="83748-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="83748-252">Additional resources</span></span>

* [<span data-ttu-id="83748-253">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83748-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83748-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83748-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

