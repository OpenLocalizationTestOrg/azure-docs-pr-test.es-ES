---
title: "Tutorial: Integración de Azure Active Directory con Panopto | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="3d29b-103">Tutorial: Integración de Azure Active Directory con Panopto</span><span class="sxs-lookup"><span data-stu-id="3d29b-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="3d29b-104">En este tutorial, aprenderá a integrar Panopto con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d29b-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d29b-105">La integración de Panopto con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3d29b-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d29b-106">Puede controlar en Azure AD quién tiene acceso a Panopto.</span><span class="sxs-lookup"><span data-stu-id="3d29b-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="3d29b-107">Puede permitir que los usuarios inicien sesión automáticamente en Panopto (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d29b-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d29b-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3d29b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3d29b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d29b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d29b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3d29b-110">Prerequisites</span></span>

<span data-ttu-id="3d29b-111">Para configurar la integración de Azure AD con Panopto, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3d29b-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="3d29b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d29b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d29b-113">Una suscripción habilitada para el inicio de sesión único en Panopto</span><span class="sxs-lookup"><span data-stu-id="3d29b-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d29b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3d29b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d29b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3d29b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d29b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3d29b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d29b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d29b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d29b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3d29b-118">Scenario description</span></span>
<span data-ttu-id="3d29b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3d29b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d29b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3d29b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d29b-121">Adición de Panopto desde la galería</span><span class="sxs-lookup"><span data-stu-id="3d29b-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="3d29b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d29b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="3d29b-123">Adición de Panopto desde la galería</span><span class="sxs-lookup"><span data-stu-id="3d29b-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="3d29b-124">Para configurar la integración de Panopto en Azure AD, es preciso agregar dicha solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3d29b-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d29b-125">**Para agregar Panopto desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d29b-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d29b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d29b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d29b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3d29b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d29b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3d29b-133">En el cuadro de búsqueda, escriba **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-133">In the search box, type **Panopto**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="3d29b-135">En el panel de resultados, seleccione **Panopto** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d29b-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d29b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d29b-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3d29b-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Panopto con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d29b-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d29b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Panopto para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d29b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="3d29b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Panopto.</span><span class="sxs-lookup"><span data-stu-id="3d29b-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="3d29b-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Panopto.</span><span class="sxs-lookup"><span data-stu-id="3d29b-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3d29b-142">Para configurar y probar el inicio de sesión único de Azure AD con Panopto, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3d29b-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d29b-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3d29b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d29b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d29b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d29b-145">**[Creación de un usuario de prueba de Panopto](#creating-a-panopto-test-user)**: el objetivo es tener un homólogo de Britta Simon en Panopto que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d29b-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d29b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d29b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d29b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3d29b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d29b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d29b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d29b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configura en la aplicación Panopto.</span><span class="sxs-lookup"><span data-stu-id="3d29b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="3d29b-150">**Para configurar el inicio de sesión único de Azure AD con Panopto, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d29b-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="3d29b-151">En la página de integración de la aplicación **Panopto** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3d29b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3d29b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="3d29b-155">En la sección **Dominio y direcciones URL de Panopto**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3d29b-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="3d29b-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.panopto.com`.</span><span class="sxs-lookup"><span data-stu-id="3d29b-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d29b-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="3d29b-158">This value is not real.</span></span> <span data-ttu-id="3d29b-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="3d29b-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3d29b-160">Póngase en contacto con el [equipo de atención al cliente de Panopto](mailto:support@panopto.com‎) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="3d29b-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="3d29b-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3d29b-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="3d29b-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3d29b-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3d29b-165">En la sección **Configuración de Panopto**, haga clic en **Configurar Panopto** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3d29b-166">Copie los valores de **identificador de entidad de SAML y dirección URL del servicio de inicio de sesión único de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="3d29b-168">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Panopto como administrador.</span><span class="sxs-lookup"><span data-stu-id="3d29b-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="3d29b-169">En la barra de herramientas de la izquierda, haga clic en **Sistema** y, luego, en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="3d29b-170">![Sistema](./media/active-directory-saas-panopto-tutorial/ic777670.png "Sistema")</span><span class="sxs-lookup"><span data-stu-id="3d29b-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="3d29b-171">Haga clic en **Agregar proveedor**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="3d29b-172">![Proveedores de identidades](./media/active-directory-saas-panopto-tutorial/ic777671.png "Proveedores de identidades")</span><span class="sxs-lookup"><span data-stu-id="3d29b-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="3d29b-173">En la sección de del proveedor SAML, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3d29b-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="3d29b-174">![Configuración de SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Configuración de SaaS")</span><span class="sxs-lookup"><span data-stu-id="3d29b-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="3d29b-175">a.</span><span class="sxs-lookup"><span data-stu-id="3d29b-175">a.</span></span> <span data-ttu-id="3d29b-176">En la lista **Tipo de proveedor**, seleccione **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="3d29b-177">b.</span><span class="sxs-lookup"><span data-stu-id="3d29b-177">b.</span></span> <span data-ttu-id="3d29b-178">En el cuadro de texto **Nombre de instancia** , escriba un nombre para la instancia.</span><span class="sxs-lookup"><span data-stu-id="3d29b-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="3d29b-179">c.</span><span class="sxs-lookup"><span data-stu-id="3d29b-179">c.</span></span> <span data-ttu-id="3d29b-180">En el cuadro de texto **Descripción detallada** , escriba una descripción detallada.</span><span class="sxs-lookup"><span data-stu-id="3d29b-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="3d29b-181">d.</span><span class="sxs-lookup"><span data-stu-id="3d29b-181">d.</span></span> <span data-ttu-id="3d29b-182">En el cuadro de texto **Bounce Page Url** (Dirección de la página de rebote), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3d29b-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3d29b-183">e.</span><span class="sxs-lookup"><span data-stu-id="3d29b-183">e.</span></span> <span data-ttu-id="3d29b-184">En el cuadro de texto **Issuer** (Emisor), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3d29b-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3d29b-185">f.</span><span class="sxs-lookup"><span data-stu-id="3d29b-185">f.</span></span> <span data-ttu-id="3d29b-186">Abra el certificado codificado en base 64 descargado de Azure Portal, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Public Key** (Clave pública).</span><span class="sxs-lookup"><span data-stu-id="3d29b-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="3d29b-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3d29b-188">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d29b-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d29b-189">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3d29b-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d29b-190">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d29b-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d29b-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d29b-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="3d29b-192">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d29b-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3d29b-194">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3d29b-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d29b-195">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d29b-197">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d29b-199">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d29b-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d29b-201">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3d29b-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d29b-203">a.</span><span class="sxs-lookup"><span data-stu-id="3d29b-203">a.</span></span> <span data-ttu-id="3d29b-204">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d29b-205">b.</span><span class="sxs-lookup"><span data-stu-id="3d29b-205">b.</span></span> <span data-ttu-id="3d29b-206">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d29b-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d29b-207">c.</span><span class="sxs-lookup"><span data-stu-id="3d29b-207">c.</span></span> <span data-ttu-id="3d29b-208">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3d29b-209">d.</span><span class="sxs-lookup"><span data-stu-id="3d29b-209">d.</span></span> <span data-ttu-id="3d29b-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="3d29b-211">Creación de un usuario de prueba de Panopto</span><span class="sxs-lookup"><span data-stu-id="3d29b-211">Creating a Panopto test user</span></span>

<span data-ttu-id="3d29b-212">No hay elemento de acción para que configure el aprovisionamiento de usuarios en Panopto.</span><span class="sxs-lookup"><span data-stu-id="3d29b-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="3d29b-213">Cuando un usuario asignado intenta iniciar sesión en Panopto desde el Panel de acceso, Panopto comprueba si el usuario existe.</span><span class="sxs-lookup"><span data-stu-id="3d29b-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="3d29b-214">Si no hay cuentas de usuario disponibles, Panopto crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3d29b-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="3d29b-215">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Panopto ofrecida por Panopto para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d29b-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3d29b-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d29b-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3d29b-217">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Panopto.</span><span class="sxs-lookup"><span data-stu-id="3d29b-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3d29b-219">**Para asignar a Britta Simon a Panopto, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d29b-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="3d29b-220">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3d29b-222">En la lista de aplicaciones, seleccione **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-222">In the applications list, select **Panopto**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="3d29b-224">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3d29b-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-226">Click **Add** button.</span></span> <span data-ttu-id="3d29b-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3d29b-229">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3d29b-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d29b-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d29b-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3d29b-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d29b-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3d29b-232">Testing single sign-on</span></span>

<span data-ttu-id="3d29b-233">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3d29b-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3d29b-234">Al hacer clic en el icono de Panopto en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d29b-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="3d29b-235">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d29b-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d29b-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3d29b-236">Additional resources</span></span>

* [<span data-ttu-id="3d29b-237">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d29b-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d29b-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d29b-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

