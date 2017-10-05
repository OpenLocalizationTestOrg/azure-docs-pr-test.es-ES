---
title: "Tutorial: Integración de Azure Active Directory con Zoom | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Zoom."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: aab491f162fd4d24c6ff4d8858f2edd96dda30d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="5b2f8-103">Tutorial: Integración de Azure Active Directory con Zoom</span><span class="sxs-lookup"><span data-stu-id="5b2f8-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="5b2f8-104">En este tutorial, obtendrá información sobre cómo integrar Zoom con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b2f8-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b2f8-105">La integración de Zoom con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b2f8-106">En Azure AD se puede controlar quién tiene acceso a Zoom.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="5b2f8-107">Puede permitir que los usuarios inicien sesión automáticamente en Zoom (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5b2f8-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5b2f8-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b2f8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b2f8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5b2f8-110">Prerequisites</span></span>

<span data-ttu-id="5b2f8-111">Para configurar la integración de Azure AD con Zoom, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="5b2f8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b2f8-113">Una suscripción habilitada para el inicio de sesión único en Zoo</span><span class="sxs-lookup"><span data-stu-id="5b2f8-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b2f8-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b2f8-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b2f8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b2f8-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b2f8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b2f8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5b2f8-118">Scenario description</span></span>
<span data-ttu-id="5b2f8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b2f8-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b2f8-121">Adición de Zoom desde la galería</span><span class="sxs-lookup"><span data-stu-id="5b2f8-121">Adding Zoom from the gallery</span></span>
2. <span data-ttu-id="5b2f8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="5b2f8-123">Adición de Zoom desde la galería</span><span class="sxs-lookup"><span data-stu-id="5b2f8-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="5b2f8-124">Para configurar la integración de Zoom en Azure AD, deberá agregar Zoom desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b2f8-125">**Para agregar Zoom desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5b2f8-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b2f8-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="5b2f8-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b2f8-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="5b2f8-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="5b2f8-133">En el cuadro de búsqueda, escriba **Zoom**, seleccione **Zoom** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![Zoom en la lista de resultados](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5b2f8-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2f8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5b2f8-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Zoom con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b2f8-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b2f8-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Zoom para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="5b2f8-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Zoom.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="5b2f8-139">Para establecer la relación de vínculo, en Zoom, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5b2f8-140">Para configurar y probar el inicio de sesión único de Azure AD con Zoom, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b2f8-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b2f8-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b2f8-143">**[Creación de un usuario de prueba de Zoom](#create-a-zoom-test-user)** : para tener un homólogo de Britta Simon en Zoom que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b2f8-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b2f8-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5b2f8-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2f8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5b2f8-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Zoom.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="5b2f8-148">**Para configurar el inicio de sesión único de Azure AD con Zoom, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5b2f8-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="5b2f8-149">En Azure Portal, en la página de integración de la aplicación **Zoom**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="5b2f8-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="5b2f8-153">En la sección **Dominio y direcciones URL de Zoom**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="5b2f8-155">a.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-155">a.</span></span> <span data-ttu-id="5b2f8-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.zoom.us`.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="5b2f8-157">b.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-157">b.</span></span> <span data-ttu-id="5b2f8-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="5b2f8-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b2f8-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-159">These values are not real.</span></span> <span data-ttu-id="5b2f8-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5b2f8-161">Contacte con el [equipo de soporte al cliente de Zoom](https://support.zoom.us/hc) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span> 
 
4. <span data-ttu-id="5b2f8-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="5b2f8-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5b2f8-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b2f8-166">En la sección **Configuración de Zoom**, haga clic en **Configurar Zoom** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-166">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5b2f8-167">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="5b2f8-169">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Zoom como administrador.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-169">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="5b2f8-170">Haga clic en la pestaña **Inicio de sesión único** .</span><span class="sxs-lookup"><span data-stu-id="5b2f8-170">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="5b2f8-171">![Pestaña de Inicio de sesión único](./media/active-directory-saas-zoom-tutorial/IC784700.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="5b2f8-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="5b2f8-172">Haga clic en la pestaña **Control de seguridad** y luego vaya a la configuración de **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-172">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="5b2f8-173">En la sección Inicio de sesión único, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-173">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="5b2f8-174">![Sección de Inicio de sesión único](./media/active-directory-saas-zoom-tutorial/IC784701.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="5b2f8-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="5b2f8-175">a.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-175">a.</span></span> <span data-ttu-id="5b2f8-176">Copie el valor de **SAML Single Sign-On Service URL** (Dirección URL de inicio de sesión único de SAML) que ha copiado de Azure Portal en el cuadro de texto **Sign-in page URL** (Dirección URL de la página de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="5b2f8-176">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="5b2f8-177">b.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-177">b.</span></span> <span data-ttu-id="5b2f8-178">En el cuadro de texto **Sign-out page URL** (Dirección URL de la página de cierre de sesión), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-178">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="5b2f8-179">c.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-179">c.</span></span> <span data-ttu-id="5b2f8-180">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de proveedor de identidades** .</span><span class="sxs-lookup"><span data-stu-id="5b2f8-180">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="5b2f8-181">d.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-181">d.</span></span> <span data-ttu-id="5b2f8-182">En el cuadro de texto **Issuer** (Emisor), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-182">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="5b2f8-183">e.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-183">e.</span></span> <span data-ttu-id="5b2f8-184">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5b2f8-185">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5b2f8-186">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5b2f8-187">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b2f8-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5b2f8-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2f8-188">Create an Azure AD test user</span></span>

<span data-ttu-id="5b2f8-189">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b2f8-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="5b2f8-191">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="5b2f8-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b2f8-192">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5b2f8-194">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5b2f8-196">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5b2f8-198">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-198">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5b2f8-200">a.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-200">a.</span></span> <span data-ttu-id="5b2f8-201">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b2f8-202">b.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-202">b.</span></span> <span data-ttu-id="5b2f8-203">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5b2f8-204">c.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-204">c.</span></span> <span data-ttu-id="5b2f8-205">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5b2f8-206">d.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-206">d.</span></span> <span data-ttu-id="5b2f8-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="5b2f8-208">Crear un usuario de prueba de Zoom</span><span class="sxs-lookup"><span data-stu-id="5b2f8-208">Create a Zoom test user</span></span>

<span data-ttu-id="5b2f8-209">Para permitir que los usuarios de Azure AD inicien sesión en Zoom, deben aprovisionarse en Zoom.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-209">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="5b2f8-210">En el caso de Zoom, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-210">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="5b2f8-211">Para aprovisionar una cuenta de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-211">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="5b2f8-212">Inicie sesión en su sitio de la compañía de **Zoom** como administrador.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-212">Log in to your **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="5b2f8-213">En la pestaña **Administración de cuentas** haga clic en **Administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-213">Click the **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="5b2f8-214">En la sección Administración de usuarios, haga clic en **Agregar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-214">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="5b2f8-215">![Administración de usuarios](./media/active-directory-saas-zoom-tutorial/IC784703.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="5b2f8-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="5b2f8-216">En la página **Agregar usuarios** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b2f8-216">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="5b2f8-217">![Agregar usuarios](./media/active-directory-saas-zoom-tutorial/IC784704.png "Agregar usuarios")</span><span class="sxs-lookup"><span data-stu-id="5b2f8-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="5b2f8-218">a.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-218">a.</span></span> <span data-ttu-id="5b2f8-219">Como **Tipo de usuario**, seleccione **Básico**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="5b2f8-220">b.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-220">b.</span></span> <span data-ttu-id="5b2f8-221">En el cuadro de texto **Correos electrónicos** , escriba la dirección de correo electrónico de una cuenta de Azure AD válida que quiera suministrar.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-221">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="5b2f8-222">c.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-222">c.</span></span> <span data-ttu-id="5b2f8-223">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="5b2f8-224">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Zoom que proporcione Zoom para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-224">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5b2f8-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2f8-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="5b2f8-226">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Zoom.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="5b2f8-228">**Para asignar el usuario Britta Simon a Zoom, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5b2f8-228">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="5b2f8-229">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5b2f8-231">En la lista de aplicaciones, seleccione **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-231">In the applications list, select **Zoom**.</span></span>

    ![Vínculo a Zoom en la lista de aplicaciones](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="5b2f8-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="5b2f8-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-235">Click **Add** button.</span></span> <span data-ttu-id="5b2f8-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="5b2f8-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b2f8-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b2f8-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5b2f8-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="5b2f8-241">Test single sign-on</span></span>

<span data-ttu-id="5b2f8-242">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b2f8-243">Al hacer clic en el icono de Zoom en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Zoom.</span><span class="sxs-lookup"><span data-stu-id="5b2f8-243">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b2f8-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5b2f8-244">Additional resources</span></span>

* [<span data-ttu-id="5b2f8-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b2f8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b2f8-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b2f8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

