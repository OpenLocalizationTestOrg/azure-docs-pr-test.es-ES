---
title: "Tutorial: Integración de Azure Active Directory con Gigya | Microsoft Doc"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: b65a33989a045a3e0b57fda522a9bc3b0770c7f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="07432-103">Tutorial: integración de Azure Active Directory con Gigya</span><span class="sxs-lookup"><span data-stu-id="07432-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="07432-104">En este tutorial, aprenderá a integrar Gigya con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07432-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07432-105">La integración de Gigya con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="07432-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07432-106">Puede controlar en Azure AD quién tiene acceso a Gigya</span><span class="sxs-lookup"><span data-stu-id="07432-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="07432-107">Puede permitir que los usuarios inicien sesión automáticamente en Gigya (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07432-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="07432-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="07432-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07432-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07432-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07432-110">Prerequisites</span></span>

<span data-ttu-id="07432-111">Para configurar la integración de Azure AD con Gigya, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="07432-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="07432-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07432-113">Una suscripción habilitada para el inicio de sesión único en Gigya</span><span class="sxs-lookup"><span data-stu-id="07432-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07432-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="07432-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07432-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="07432-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07432-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="07432-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07432-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07432-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07432-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="07432-118">Scenario description</span></span>
<span data-ttu-id="07432-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="07432-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07432-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="07432-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07432-121">Adición de Gigya desde la galería</span><span class="sxs-lookup"><span data-stu-id="07432-121">Adding Gigya from the gallery</span></span>
2. <span data-ttu-id="07432-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="07432-123">Adición de Gigya desde la galería</span><span class="sxs-lookup"><span data-stu-id="07432-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="07432-124">Para configurar la integración de Gigya en Azure AD, es preciso agregar Gigya desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="07432-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07432-125">**Para agregar Gigya desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="07432-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07432-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07432-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07432-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="07432-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07432-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="07432-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="07432-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07432-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="07432-133">En el cuadro de búsqueda, escriba **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="07432-133">In the search box, type **Gigya**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="07432-135">En el panel de resultados, seleccione **Gigya** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07432-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07432-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07432-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Gigya con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07432-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07432-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Gigya para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07432-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="07432-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Gigya.</span><span class="sxs-lookup"><span data-stu-id="07432-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="07432-141">Para establecer la relación de vínculo en Gigya, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="07432-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07432-142">Para configurar y probar el inicio de sesión único de Azure AD con Gigya, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="07432-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07432-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="07432-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07432-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07432-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07432-145">**[Creación de un usuario de prueba de Gigya](#creating-a-gigya-test-user)**: para tener un homólogo de Britta Simon en Gigya que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="07432-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07432-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07432-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07432-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="07432-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07432-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07432-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Gigya.</span><span class="sxs-lookup"><span data-stu-id="07432-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="07432-150">**Para configurar el inicio de sesión único de Azure AD con Gigya, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="07432-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="07432-151">En Azure Portal, en la página de integración de la aplicación **Gigya**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="07432-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="07432-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="07432-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="07432-155">En la sección **Dominio y direcciones URL de Gigya**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="07432-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="07432-157">a.</span><span class="sxs-lookup"><span data-stu-id="07432-157">a.</span></span> <span data-ttu-id="07432-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `http://<companyname>.gigya.com`.</span><span class="sxs-lookup"><span data-stu-id="07432-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="07432-159">b.</span><span class="sxs-lookup"><span data-stu-id="07432-159">b.</span></span> <span data-ttu-id="07432-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="07432-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07432-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="07432-161">These values are not real.</span></span> <span data-ttu-id="07432-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="07432-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="07432-163">Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de clientes de Gigya](https://www.gigya.com/support-policy/).</span><span class="sxs-lookup"><span data-stu-id="07432-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
4. <span data-ttu-id="07432-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="07432-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="07432-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="07432-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="07432-168">En la sección **Configuración de Gigya**, haga clic en **Configurar Gigya** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="07432-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07432-169">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="07432-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="07432-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Gigya como administrador.</span><span class="sxs-lookup"><span data-stu-id="07432-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="07432-172">Vaya **Settings \> SAML Login** (Configuración > Inicio de sesión de SAML), y luego haga clic en el botón **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="07432-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="07432-173">![Inicio de sesión SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "Inicio de sesión SAML")</span><span class="sxs-lookup"><span data-stu-id="07432-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="07432-174">En la sección **Inicio de sesión de SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="07432-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="07432-175">![Configuración de SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="07432-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="07432-176">a.</span><span class="sxs-lookup"><span data-stu-id="07432-176">a.</span></span> <span data-ttu-id="07432-177">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración.</span><span class="sxs-lookup"><span data-stu-id="07432-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="07432-178">b.</span><span class="sxs-lookup"><span data-stu-id="07432-178">b.</span></span> <span data-ttu-id="07432-179">En el cuadro de texto **Emisor**, pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="07432-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="07432-180">c.</span><span class="sxs-lookup"><span data-stu-id="07432-180">c.</span></span> <span data-ttu-id="07432-181">En el cuadro de texto **Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único), pegue el valor de 
**Dirección URL del servicio de inicio de sesión único** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="07432-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="07432-182">d.</span><span class="sxs-lookup"><span data-stu-id="07432-182">d.</span></span> <span data-ttu-id="07432-183">En el cuadro de texto **Name ID Format** (Formato de id. de nombre), pegue el valor de **Formato de identificador de nombre** que haya copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="07432-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="07432-184">e.</span><span class="sxs-lookup"><span data-stu-id="07432-184">e.</span></span> <span data-ttu-id="07432-185">Abra el certificado codificado en base 64 descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="07432-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="07432-186">f.</span><span class="sxs-lookup"><span data-stu-id="07432-186">f.</span></span> <span data-ttu-id="07432-187">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="07432-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="07432-188">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07432-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07432-189">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="07432-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07432-190">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07432-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07432-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="07432-192">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07432-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="07432-194">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="07432-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07432-195">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07432-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07432-197">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="07432-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07432-199">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07432-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07432-201">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="07432-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07432-203">a.</span><span class="sxs-lookup"><span data-stu-id="07432-203">a.</span></span> <span data-ttu-id="07432-204">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07432-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07432-205">b.</span><span class="sxs-lookup"><span data-stu-id="07432-205">b.</span></span> <span data-ttu-id="07432-206">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07432-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07432-207">c.</span><span class="sxs-lookup"><span data-stu-id="07432-207">c.</span></span> <span data-ttu-id="07432-208">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="07432-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="07432-209">d.</span><span class="sxs-lookup"><span data-stu-id="07432-209">d.</span></span> <span data-ttu-id="07432-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="07432-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="07432-211">Creación de usuario de prueba de Gigya</span><span class="sxs-lookup"><span data-stu-id="07432-211">Creating a Gigya test user</span></span>

<span data-ttu-id="07432-212">Para permitir que los usuarios de Azure AD inicien sesión en Gigya, deben aprovisionarse en Gigya.</span><span class="sxs-lookup"><span data-stu-id="07432-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="07432-213">En el caso de Gigya, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="07432-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="07432-214">Para aprovisionar cuentas de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="07432-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="07432-215">Inicie sesión en el sitio de la compañía de **Gigya** como administrador.</span><span class="sxs-lookup"><span data-stu-id="07432-215">Log in to your **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="07432-216">Vaya a **Admin \> Manage Users** (Administrador > Administrar usuarios) y, a continuación, haga clic en **Invite Users** (Invitar a usuarios).</span><span class="sxs-lookup"><span data-stu-id="07432-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="07432-217">![Administración de usuarios](./media/active-directory-saas-gigya-tutorial/ic789535.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="07432-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="07432-218">En el cuadro de diálogo Invite Users (Invitar a usuarios), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="07432-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="07432-219">![Invitar a usuarios](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invitar a usuarios")</span><span class="sxs-lookup"><span data-stu-id="07432-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="07432-220">a.</span><span class="sxs-lookup"><span data-stu-id="07432-220">a.</span></span> <span data-ttu-id="07432-221">En el cuadro de texto **Correo electrónico** , escriba el alias de correo electrónico de la cuenta válida de Azure Active Directory que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="07432-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="07432-222">b.</span><span class="sxs-lookup"><span data-stu-id="07432-222">b.</span></span> <span data-ttu-id="07432-223">Haga clic en **Invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="07432-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="07432-224">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="07432-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="07432-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07432-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="07432-226">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Gigya.</span><span class="sxs-lookup"><span data-stu-id="07432-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="07432-228">**Para asignar el usuario Britta Simon a Gigya, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="07432-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="07432-229">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="07432-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="07432-231">En la lista de aplicaciones, seleccione **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="07432-231">In the applications list, select **Gigya**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="07432-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="07432-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="07432-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="07432-235">Click **Add** button.</span></span> <span data-ttu-id="07432-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="07432-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="07432-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="07432-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07432-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="07432-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07432-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="07432-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07432-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="07432-241">Testing single sign-on</span></span>

<span data-ttu-id="07432-242">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="07432-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="07432-243">Al hacer clic en el icono de Gigya en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Gigya.</span><span class="sxs-lookup"><span data-stu-id="07432-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07432-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="07432-244">Additional resources</span></span>

* [<span data-ttu-id="07432-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07432-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07432-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07432-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

