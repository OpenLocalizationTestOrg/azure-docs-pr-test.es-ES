---
title: "Tutorial: Integración de Azure Active Directory con ITRP | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: fae1c7b6b0e04c1e23123d3aee7913cb3131e645
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="1fcba-103">Tutorial: Integración de Azure Active Directory con ITRP</span><span class="sxs-lookup"><span data-stu-id="1fcba-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="1fcba-104">En este tutorial se aprende a integrar ITRP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1fcba-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fcba-105">La integración de ITRP con Azure AD le ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1fcba-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1fcba-106">Puede controlar en Azure AD quién tiene acceso a ITRP.</span><span class="sxs-lookup"><span data-stu-id="1fcba-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="1fcba-107">Puede permitir que los usuarios inicien sesión automáticamente en ITRP (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fcba-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1fcba-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1fcba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1fcba-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1fcba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fcba-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1fcba-110">Prerequisites</span></span>

<span data-ttu-id="1fcba-111">Para configurar la integración de Azure AD con ITRP, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1fcba-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="1fcba-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fcba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fcba-113">Una suscripción habilitada para el inicio de sesión único en ITRP</span><span class="sxs-lookup"><span data-stu-id="1fcba-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fcba-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1fcba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fcba-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1fcba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fcba-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1fcba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fcba-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fcba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fcba-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1fcba-118">Scenario description</span></span>
<span data-ttu-id="1fcba-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1fcba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fcba-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1fcba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fcba-121">Incorporación de ITRP desde la galería</span><span class="sxs-lookup"><span data-stu-id="1fcba-121">Adding ITRP from the gallery</span></span>
2. <span data-ttu-id="1fcba-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fcba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="1fcba-123">Incorporación de ITRP desde la galería</span><span class="sxs-lookup"><span data-stu-id="1fcba-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="1fcba-124">Para configurar la integración de ITRP en Azure AD, tiene que agregar ITRP desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1fcba-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1fcba-125">**Para agregar ITRP desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fcba-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcba-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1fcba-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1fcba-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1fcba-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fcba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1fcba-133">En el cuadro de búsqueda, escriba **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-133">In the search box, type **ITRP**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="1fcba-135">En el panel de resultados, seleccione **ITRP** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fcba-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1fcba-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fcba-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="1fcba-138">En esta sección se configura y prueba el inicio de sesión único de Azure AD con ITRP con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fcba-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1fcba-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ITRP para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fcba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="1fcba-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ITRP.</span><span class="sxs-lookup"><span data-stu-id="1fcba-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="1fcba-141">Para establecer la relación de vínculo, en ITRP, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1fcba-142">Para configurar y probar el inicio de sesión único de Azure AD con ITRP, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1fcba-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1fcba-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="1fcba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1fcba-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fcba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fcba-145">**[Creación de un usuario de prueba de ITRP](#creating-an-itrp-test-user)**: para tener un homólogo de Britta Simon en ITRP vinculado a la representación de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fcba-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1fcba-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fcba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fcba-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1fcba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1fcba-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fcba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1fcba-149">En esta sección se habilita el inicio de sesión único de Azure AD en Azure Portal y se configura el inicio de sesión único en la aplicación ITRP.</span><span class="sxs-lookup"><span data-stu-id="1fcba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="1fcba-150">**Para configurar el inicio de sesión único de Azure AD con ITRP, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fcba-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcba-151">En Azure Portal, en la página de integración de la aplicación **ITRP**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1fcba-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1fcba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="1fcba-155">En la sección **Dominio y direcciones URL de ITRP**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1fcba-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="1fcba-157">a.</span><span class="sxs-lookup"><span data-stu-id="1fcba-157">a.</span></span> <span data-ttu-id="1fcba-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.itrp.com`.</span><span class="sxs-lookup"><span data-stu-id="1fcba-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="1fcba-159">b.</span><span class="sxs-lookup"><span data-stu-id="1fcba-159">b.</span></span> <span data-ttu-id="1fcba-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="1fcba-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1fcba-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1fcba-161">These values are not real.</span></span> <span data-ttu-id="1fcba-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1fcba-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1fcba-163">Contacte con el [equipo de soporte técnico de cliente de ITRP](https://www.itrp.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="1fcba-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="1fcba-164">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="1fcba-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="1fcba-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1fcba-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1fcba-168">En la sección **Configuración de ITRP**, haga clic en **Configurar ITRP** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1fcba-169">Copie la **dirección URL del servicio de inicio de sesión único de SAML y la URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="1fcba-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de ITRP.</span><span class="sxs-lookup"><span data-stu-id="1fcba-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="1fcba-172">En la barra de herramientas de la parte superior, haga clic en el icono de **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="1fcba-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="1fcba-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="1fcba-174">En el panel de navegación izquierdo, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="1fcba-175">![Inicio de sesión único](./media/active-directory-saas-itrp-tutorial/ic775571.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1fcba-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="1fcba-176">Siga estos pasos en la sección de configuración de Single Sign-On (Inicio de sesión único):</span><span class="sxs-lookup"><span data-stu-id="1fcba-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="1fcba-177">![Inicio de sesión único](./media/active-directory-saas-itrp-tutorial/ic775572.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1fcba-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="1fcba-178">![Inicio de sesión único](./media/active-directory-saas-itrp-tutorial/ic775573.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1fcba-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="1fcba-179">a.</span><span class="sxs-lookup"><span data-stu-id="1fcba-179">a.</span></span> <span data-ttu-id="1fcba-180">Hacer clic en **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-180">Click **Enable**.</span></span>

    <span data-ttu-id="1fcba-181">b.</span><span class="sxs-lookup"><span data-stu-id="1fcba-181">b.</span></span> <span data-ttu-id="1fcba-182">En el cuadro de texto **Remote Log Out URL** (Dirección URL de cierre de sesión remoto), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1fcba-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1fcba-183">c.</span><span class="sxs-lookup"><span data-stu-id="1fcba-183">c.</span></span> <span data-ttu-id="1fcba-184">En el cuadro de texto **SAML SSO URL** (Dirección URL de inicio de sesión único de SAML), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1fcba-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1fcba-185">En el cuadro de texto **Certificate Fingerprint** (Huella digital de certificado), pegue el valor de **Huella digital** del certificado que haya copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1fcba-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="1fcba-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1fcba-187">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fcba-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1fcba-188">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1fcba-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1fcba-189">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1fcba-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1fcba-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fcba-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="1fcba-191">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fcba-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1fcba-193">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1fcba-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcba-194">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1fcba-196">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1fcba-198">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fcba-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1fcba-200">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1fcba-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1fcba-202">a.</span><span class="sxs-lookup"><span data-stu-id="1fcba-202">a.</span></span> <span data-ttu-id="1fcba-203">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fcba-204">b.</span><span class="sxs-lookup"><span data-stu-id="1fcba-204">b.</span></span> <span data-ttu-id="1fcba-205">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fcba-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1fcba-206">c.</span><span class="sxs-lookup"><span data-stu-id="1fcba-206">c.</span></span> <span data-ttu-id="1fcba-207">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1fcba-208">d.</span><span class="sxs-lookup"><span data-stu-id="1fcba-208">d.</span></span> <span data-ttu-id="1fcba-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="1fcba-210">Creación de un usuario de prueba de ITRP</span><span class="sxs-lookup"><span data-stu-id="1fcba-210">Creating an ITRP test user</span></span>

<span data-ttu-id="1fcba-211">Para permitir que los usuarios de Azure AD inicien sesión en ITRP, tienen que aprovisionarse en ITRP.</span><span class="sxs-lookup"><span data-stu-id="1fcba-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="1fcba-212">En el caso de ITRP, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="1fcba-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="1fcba-213">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1fcba-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcba-214">Inicie sesión en su inquilino de **ITRP** .</span><span class="sxs-lookup"><span data-stu-id="1fcba-214">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="1fcba-215">En la barra de herramientas de la parte superior, haga clic en el icono de **Registros**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="1fcba-216">![Administración](./media/active-directory-saas-itrp-tutorial/ic775575.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="1fcba-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="1fcba-217">En el menú emergente, seleccione **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="1fcba-218">![Personas](./media/active-directory-saas-itrp-tutorial/ic775587.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="1fcba-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="1fcba-219">Haga clic en **Agregar nueva persona** (“+”).</span><span class="sxs-lookup"><span data-stu-id="1fcba-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="1fcba-220">![Administración](./media/active-directory-saas-itrp-tutorial/ic775576.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="1fcba-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="1fcba-221">En el cuadro de diálogo Add New Person (Agregar nueva persona), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1fcba-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="1fcba-222">![Usuario](./media/active-directory-saas-itrp-tutorial/ic775577.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="1fcba-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="1fcba-223">a.</span><span class="sxs-lookup"><span data-stu-id="1fcba-223">a.</span></span> <span data-ttu-id="1fcba-224">Escriba el **nombre** y el **correo electrónico** de la cuenta válida de AAD que desee aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="1fcba-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="1fcba-225">b.</span><span class="sxs-lookup"><span data-stu-id="1fcba-225">b.</span></span> <span data-ttu-id="1fcba-226">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1fcba-227">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de ITRP que proporcione ITRP para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="1fcba-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1fcba-228">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fcba-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1fcba-229">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ITRP.</span><span class="sxs-lookup"><span data-stu-id="1fcba-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1fcba-231">**Para asignar el usuario Britta Simon a ITRP, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fcba-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcba-232">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1fcba-234">En la lista de aplicaciones, seleccione **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-234">In the applications list, select **ITRP**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="1fcba-236">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1fcba-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-238">Click **Add** button.</span></span> <span data-ttu-id="1fcba-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1fcba-241">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1fcba-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1fcba-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1fcba-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fcba-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1fcba-244">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1fcba-244">Testing single sign-on</span></span>

<span data-ttu-id="1fcba-245">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1fcba-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1fcba-246">Al hacer clic en el icono de ITRP en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de ITRP.</span><span class="sxs-lookup"><span data-stu-id="1fcba-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="1fcba-247">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1fcba-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fcba-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1fcba-248">Additional resources</span></span>

* [<span data-ttu-id="1fcba-249">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fcba-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fcba-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fcba-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

