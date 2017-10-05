---
title: "Tutorial: Integración de Azure Active Directory con Halogen Software | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Halogen Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="92cc5-103">Tutorial: Integración de Azure Active Directory con Halogen Software</span><span class="sxs-lookup"><span data-stu-id="92cc5-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="92cc5-104">En este tutorial, aprenderá a integrar Halogen Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92cc5-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92cc5-105">La integración de Halogen Software con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="92cc5-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92cc5-106">Puede controlar en Azure AD quién tiene acceso a Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="92cc5-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="92cc5-107">Puede permitir que los usuarios inicien sesión automáticamente en Halogen Software (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92cc5-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92cc5-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="92cc5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92cc5-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92cc5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92cc5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="92cc5-110">Prerequisites</span></span>

<span data-ttu-id="92cc5-111">Para configurar la integración de Azure AD con Halogen Software, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="92cc5-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="92cc5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cc5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92cc5-113">Un suscripción habilitada para el inicio de sesión único en Halogen Software</span><span class="sxs-lookup"><span data-stu-id="92cc5-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92cc5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="92cc5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92cc5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="92cc5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92cc5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="92cc5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92cc5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92cc5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92cc5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="92cc5-118">Scenario description</span></span>

<span data-ttu-id="92cc5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="92cc5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92cc5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="92cc5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92cc5-121">Agregar Halogen Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="92cc5-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="92cc5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cc5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="92cc5-123">Agregar Halogen Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="92cc5-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="92cc5-124">Para configurar la integración de Halogen Software en Azure AD, deberá agregar Halogen Software desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="92cc5-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92cc5-125">**Para agregar Halogen Software desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="92cc5-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92cc5-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92cc5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92cc5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="92cc5-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92cc5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="92cc5-133">En el cuadro de búsqueda, escriba **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-133">In the search box, type **Halogen Software**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="92cc5-135">En el panel de resultados, seleccione **Halogen Software** y haga clic en **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92cc5-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92cc5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cc5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92cc5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Halogen Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="92cc5-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92cc5-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Halogen Software para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92cc5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="92cc5-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="92cc5-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="92cc5-141">En Halogen Software, asigne el valor del **nombre de usuario** en Azure AD como valor de **nombre de usuario** para establecer la relación de vínculo.</span><span class="sxs-lookup"><span data-stu-id="92cc5-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92cc5-142">Para configurar y probar el inicio de sesión único de Azure AD con Halogen Software, debe completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="92cc5-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92cc5-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="92cc5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92cc5-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92cc5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92cc5-145">**[Creación de un usuario de prueba de Halogen Software](#creating-a-halogen-software-test-user)** : para tener un homólogo de Britta Simon en Halogen Software que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92cc5-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92cc5-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92cc5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92cc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="92cc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92cc5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cc5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92cc5-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="92cc5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="92cc5-150">**Para configurar el inicio de sesión único de Azure AD con Halogen Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="92cc5-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="92cc5-151">En Azure Portal, en la página de integración de la aplicación **Halogen Software**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="92cc5-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="92cc5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="92cc5-155">En la sección **Dominio y direcciones URL de Halogen Software**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="92cc5-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="92cc5-157">a.</span><span class="sxs-lookup"><span data-stu-id="92cc5-157">a.</span></span> <span data-ttu-id="92cc5-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://global.hgncloud.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="92cc5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="92cc5-159">b.</span><span class="sxs-lookup"><span data-stu-id="92cc5-159">b.</span></span> <span data-ttu-id="92cc5-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="92cc5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92cc5-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="92cc5-161">These values are not real.</span></span> <span data-ttu-id="92cc5-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="92cc5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92cc5-163">Para obtener estos valores, póngase en contacto con el [equipo de soporte de cliente de Halogen Software](https://support.halogensoftware.com/).</span><span class="sxs-lookup"><span data-stu-id="92cc5-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="92cc5-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="92cc5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="92cc5-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="92cc5-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92cc5-168">En una ventana de explorador diferente, inicie sesión en su aplicación de **Halogen Software** como administrador.</span><span class="sxs-lookup"><span data-stu-id="92cc5-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="92cc5-169">Haga clic en la pestaña **Opciones** .</span><span class="sxs-lookup"><span data-stu-id="92cc5-169">Click the **Options** tab.</span></span> 
   
    ![Qué es Azure AD Connect][12]

8. <span data-ttu-id="92cc5-171">En el panel de navegación izquierdo, haga clic en **Configuración de SAML**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Qué es Azure AD Connect][13]

9. <span data-ttu-id="92cc5-173">En la página **Configuración de SAML** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="92cc5-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Qué es Azure AD Connect][14]

     <span data-ttu-id="92cc5-175">a.</span><span class="sxs-lookup"><span data-stu-id="92cc5-175">a.</span></span> <span data-ttu-id="92cc5-176">En **Identificador único**, seleccione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="92cc5-177">b.</span><span class="sxs-lookup"><span data-stu-id="92cc5-177">b.</span></span> <span data-ttu-id="92cc5-178">En **El identificador único se asigna a**, seleccione **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="92cc5-179">c.</span><span class="sxs-lookup"><span data-stu-id="92cc5-179">c.</span></span> <span data-ttu-id="92cc5-180">Para cargar el archivo de metadatos descargado, haga clic en **Examinar** para seleccionar el archivo y en **Cargar archivo**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="92cc5-181">d.</span><span class="sxs-lookup"><span data-stu-id="92cc5-181">d.</span></span> <span data-ttu-id="92cc5-182">Para probar la configuración, haga clic en **Ejecutar prueba**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="92cc5-183">Deberá esperar a que aparezca el mensaje "*La prueba de SAML está completa. Cierre esta ventana* ".</span><span class="sxs-lookup"><span data-stu-id="92cc5-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="92cc5-184">A continuación, cierre la ventana del explorador abierta.</span><span class="sxs-lookup"><span data-stu-id="92cc5-184">Then, close the opened browser window.</span></span> <span data-ttu-id="92cc5-185">La casilla de verificación **Habilitar SAML** solo está habilitada si se ha completado la prueba.</span><span class="sxs-lookup"><span data-stu-id="92cc5-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="92cc5-186">e.</span><span class="sxs-lookup"><span data-stu-id="92cc5-186">e.</span></span> <span data-ttu-id="92cc5-187">Seleccione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="92cc5-188">f.</span><span class="sxs-lookup"><span data-stu-id="92cc5-188">f.</span></span> <span data-ttu-id="92cc5-189">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="92cc5-190">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92cc5-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92cc5-191">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="92cc5-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92cc5-192">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92cc5-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92cc5-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cc5-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="92cc5-194">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="92cc5-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="92cc5-196">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="92cc5-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92cc5-197">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92cc5-199">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92cc5-201">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92cc5-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92cc5-203">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="92cc5-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92cc5-205">a.</span><span class="sxs-lookup"><span data-stu-id="92cc5-205">a.</span></span> <span data-ttu-id="92cc5-206">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="92cc5-207">b.</span><span class="sxs-lookup"><span data-stu-id="92cc5-207">b.</span></span> <span data-ttu-id="92cc5-208">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92cc5-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92cc5-209">c.</span><span class="sxs-lookup"><span data-stu-id="92cc5-209">c.</span></span> <span data-ttu-id="92cc5-210">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92cc5-211">d.</span><span class="sxs-lookup"><span data-stu-id="92cc5-211">d.</span></span> <span data-ttu-id="92cc5-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="92cc5-213">Creación de un usuario de prueba de Halogen Software</span><span class="sxs-lookup"><span data-stu-id="92cc5-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="92cc5-214">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="92cc5-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="92cc5-215">**Para crear un usuario llamado Britta Simon en Halogen Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="92cc5-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="92cc5-216">Inicie sesión en su aplicación de **Halogen Software** como administrador.</span><span class="sxs-lookup"><span data-stu-id="92cc5-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="92cc5-217">Haga clic en la pestaña **Centro de usuarios** y en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Qué es Azure AD Connect][300]  

3. <span data-ttu-id="92cc5-219">En la página del cuadro de diálogo **Nuevo usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="92cc5-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Qué es Azure AD Connect][301]

    <span data-ttu-id="92cc5-221">a.</span><span class="sxs-lookup"><span data-stu-id="92cc5-221">a.</span></span> <span data-ttu-id="92cc5-222">En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="92cc5-223">b.</span><span class="sxs-lookup"><span data-stu-id="92cc5-223">b.</span></span> <span data-ttu-id="92cc5-224">En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="92cc5-225">c.</span><span class="sxs-lookup"><span data-stu-id="92cc5-225">c.</span></span> <span data-ttu-id="92cc5-226">En el cuadro de texto **Nombre de usuario**, escriba el nombre de usuario **Britta Simon** como en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="92cc5-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="92cc5-227">d.</span><span class="sxs-lookup"><span data-stu-id="92cc5-227">d.</span></span> <span data-ttu-id="92cc5-228">En el cuadro de texto **Contraseña** , escriba una contraseña para Britta.</span><span class="sxs-lookup"><span data-stu-id="92cc5-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="92cc5-229">e.</span><span class="sxs-lookup"><span data-stu-id="92cc5-229">e.</span></span> <span data-ttu-id="92cc5-230">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92cc5-231">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cc5-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92cc5-232">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="92cc5-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="92cc5-234">**Para asignar un usuario llamado Britta Simon a Halogen Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="92cc5-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="92cc5-235">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="92cc5-237">En la lista de aplicaciones, seleccione **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-237">In the applications list, select **Halogen Software**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="92cc5-239">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="92cc5-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-241">Click **Add** button.</span></span> <span data-ttu-id="92cc5-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="92cc5-244">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="92cc5-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92cc5-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92cc5-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="92cc5-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92cc5-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="92cc5-247">Testing single sign-on</span></span>

<span data-ttu-id="92cc5-248">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="92cc5-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="92cc5-249">Al hacer clic en el icono de Halogen Software en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación de Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="92cc5-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92cc5-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="92cc5-250">Additional resources</span></span>

* [<span data-ttu-id="92cc5-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92cc5-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92cc5-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92cc5-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
