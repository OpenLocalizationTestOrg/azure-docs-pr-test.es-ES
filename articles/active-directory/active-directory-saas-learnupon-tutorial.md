---
title: "Tutorial: Integración de Azure Active Directory con LearnUpon | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="ae69f-103">Tutorial: Integración de Azure Active Directory con LearnUpon</span><span class="sxs-lookup"><span data-stu-id="ae69f-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="ae69f-104">En este tutorial, aprenderá a integrar LearnUpon con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae69f-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae69f-105">La integración de LearnUpon con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ae69f-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae69f-106">En Azure AD se puede controlar quién tiene acceso a LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="ae69f-107">Puede permitir que los usuarios inicien sesión automáticamente en LearnUpon (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae69f-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae69f-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ae69f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae69f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae69f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae69f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ae69f-110">Prerequisites</span></span>

<span data-ttu-id="ae69f-111">Para configurar la integración de Azure AD con LearnUpon, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ae69f-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="ae69f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae69f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae69f-113">Una suscripción habilitada para el inicio de sesión único en LearnUpon</span><span class="sxs-lookup"><span data-stu-id="ae69f-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae69f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ae69f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae69f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ae69f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae69f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ae69f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae69f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae69f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae69f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ae69f-118">Scenario description</span></span>
<span data-ttu-id="ae69f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ae69f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae69f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ae69f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae69f-121">Incorporación de LearnUpon desde la galería</span><span class="sxs-lookup"><span data-stu-id="ae69f-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="ae69f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae69f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="ae69f-123">Incorporación de LearnUpon desde la galería</span><span class="sxs-lookup"><span data-stu-id="ae69f-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="ae69f-124">Para configurar la integración de LearnUpon en Azure AD, es preciso agregar LearnUpon desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ae69f-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae69f-125">**Para agregar LearnUpon desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ae69f-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae69f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae69f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae69f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ae69f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae69f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ae69f-133">En el cuadro de búsqueda, escriba **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-133">In the search box, type **LearnUpon**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="ae69f-135">En el panel de resultados, seleccione **LearnUpon** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae69f-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae69f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae69f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae69f-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LearnUpon con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae69f-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae69f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LearnUpon para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae69f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="ae69f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="ae69f-141">Para establecer la relación de vínculo, en LearnUpon, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae69f-142">Para configurar y probar el inicio de sesión único de Azure AD con LearnUpon, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ae69f-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae69f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="ae69f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae69f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae69f-145">**[Creación de un usuario de prueba de LearnUpon](#creating-a-learnupon-test-user)**: el objetivo es tener un homólogo de Britta Simon en LearnUpon que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae69f-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae69f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae69f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae69f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ae69f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae69f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae69f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae69f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="ae69f-150">**Para configurar el inicio de sesión único de Azure AD con LearnUpon, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ae69f-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="ae69f-151">En la página de integración de la aplicación **LearnUpon** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ae69f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ae69f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="ae69f-155">En la sección **Dominio y direcciones URL de LearnUpon**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ae69f-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="ae69f-157">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.learnupon.com/saml/consumer`.</span><span class="sxs-lookup"><span data-stu-id="ae69f-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae69f-158">Tenga en cuenta que este no es el valor real.</span><span class="sxs-lookup"><span data-stu-id="ae69f-158">Please note that this is not the real value.</span></span> <span data-ttu-id="ae69f-159">Tendrá que actualizar este valor con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="ae69f-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="ae69f-160">Para obtener este valor, póngase en contacto con el [equipo de soporte técnico de LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="ae69f-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="ae69f-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (sin procesar)** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ae69f-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="ae69f-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ae69f-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ae69f-165">En la sección **Configuración de LearnUpon**, haga clic en **Configurar LearnUpon** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ae69f-166">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="ae69f-168">Abra otra instancia del explorador e inicie sesión en LearnUpon con una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="ae69f-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="ae69f-169">Haga clic en la pestaña **settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="ae69f-169">Click the **settings** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="ae69f-171">Haga clic en **Single Sign On - SAML** (Inicio de sesión único - SAML) y, después, en **General Settings** (Configuración general) para configurar SAML.</span><span class="sxs-lookup"><span data-stu-id="ae69f-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="ae69f-173">En la sección **General Settings** (Configuración general), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ae69f-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="ae69f-175">a.</span><span class="sxs-lookup"><span data-stu-id="ae69f-175">a.</span></span> <span data-ttu-id="ae69f-176">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-176">Select **Enabled**.</span></span>

    <span data-ttu-id="ae69f-177">b.</span><span class="sxs-lookup"><span data-stu-id="ae69f-177">b.</span></span> <span data-ttu-id="ae69f-178">Seleccione la **versión** **2.0**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="ae69f-179">c.</span><span class="sxs-lookup"><span data-stu-id="ae69f-179">c.</span></span> <span data-ttu-id="ae69f-180">En **Skip conditions** (Omitir condiciones), haga clic en **No**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="ae69f-181">d.</span><span class="sxs-lookup"><span data-stu-id="ae69f-181">d.</span></span> <span data-ttu-id="ae69f-182">En el cuadro de texto **SAML Token Post param name** (Nombre de parámetro POST de token SAML), escriba el nombre del parámetro POST de la solicitud en la dirección URL del consumidor de SAML indicada anteriormente que contenga la aserción SAML que se va a comprobar y autenticar (por ejemplo, **SAMLResponse**).</span><span class="sxs-lookup"><span data-stu-id="ae69f-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="ae69f-183">e.</span><span class="sxs-lookup"><span data-stu-id="ae69f-183">e.</span></span> <span data-ttu-id="ae69f-184">En el cuadro de texto **Name Identifier Format** (Formato de identificador de nombre), escriba el valor que indica en qué lugar de la aserción SAML reside el identificador del usuario (dirección de correo electrónico) (por ejemplo, **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**).</span><span class="sxs-lookup"><span data-stu-id="ae69f-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="ae69f-185">f.</span><span class="sxs-lookup"><span data-stu-id="ae69f-185">f.</span></span> <span data-ttu-id="ae69f-186">En el cuadro de texto **Identify Provider Location** (Identificar la ubicación del proveedor), escriba el valor que indica el lugar al que se envían los usuarios si hacen clic en el icono cargado desde la pantalla de inicio de sesión de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ae69f-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="ae69f-187">g.</span><span class="sxs-lookup"><span data-stu-id="ae69f-187">g.</span></span> <span data-ttu-id="ae69f-188">En el cuadro de texto **Sign out URL** (Dirección URL de cierre de sesión), pegue la **URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ae69f-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="ae69f-189">h.</span><span class="sxs-lookup"><span data-stu-id="ae69f-189">h.</span></span> <span data-ttu-id="ae69f-190">Haga clic en **Manage finger prints**(Administrar huellas dactilares) y, a continuación, cargue la huella digital del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="ae69f-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="ae69f-191">Haga clic en **User Settings**(Configuración del usuario) y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ae69f-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="ae69f-193">a.</span><span class="sxs-lookup"><span data-stu-id="ae69f-193">a.</span></span> <span data-ttu-id="ae69f-194">En el cuadro de texto **First Name Identifier Format** (Formato de identificador de nombre), escriba el valor que nos indica el lugar de la aserción SAML en que reside el nombre de los usuarios (por ejemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname)**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="ae69f-195">b.</span><span class="sxs-lookup"><span data-stu-id="ae69f-195">b.</span></span> <span data-ttu-id="ae69f-196">En el cuadro de texto **Last Name Identifier Format** (Formato de identificador de apellido), escriba el valor que nos indica el lugar de la aserción SAML en que residen los apellidos de los usuarios (por ejemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname)**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="ae69f-197">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae69f-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae69f-198">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ae69f-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae69f-199">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae69f-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae69f-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae69f-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae69f-201">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae69f-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ae69f-203">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ae69f-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae69f-204">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae69f-206">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae69f-208">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae69f-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae69f-210">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ae69f-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae69f-212">a.</span><span class="sxs-lookup"><span data-stu-id="ae69f-212">a.</span></span> <span data-ttu-id="ae69f-213">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae69f-214">b.</span><span class="sxs-lookup"><span data-stu-id="ae69f-214">b.</span></span> <span data-ttu-id="ae69f-215">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae69f-216">c.</span><span class="sxs-lookup"><span data-stu-id="ae69f-216">c.</span></span> <span data-ttu-id="ae69f-217">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae69f-218">d.</span><span class="sxs-lookup"><span data-stu-id="ae69f-218">d.</span></span> <span data-ttu-id="ae69f-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="ae69f-220">Creación de un usuario de prueba de LearnUpon</span><span class="sxs-lookup"><span data-stu-id="ae69f-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="ae69f-221">El objetivo de esta sección es crear un usuario llamado Britta Simon en LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="ae69f-222">LearnUpon admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ae69f-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ae69f-223">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="ae69f-223">There is no action item for you in this section.</span></span> <span data-ttu-id="ae69f-224">Durante un intento de acceder a LearnUpon se creará un nuevo usuario, si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="ae69f-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="ae69f-225">[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ae69f-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="ae69f-226">Si necesita crear un usuario manualmente, es preciso que se ponga contacto con el [equipo de soporte técnico de LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="ae69f-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae69f-227">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae69f-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae69f-228">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ae69f-230">**Para asignar Britta Simon a LearnUpon, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ae69f-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="ae69f-231">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ae69f-233">En la lista de aplicaciones, seleccione **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-233">In the applications list, select **LearnUpon**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="ae69f-235">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ae69f-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-237">Click **Add** button.</span></span> <span data-ttu-id="ae69f-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ae69f-240">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ae69f-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae69f-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae69f-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae69f-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae69f-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ae69f-243">Testing single sign-on</span></span>

<span data-ttu-id="ae69f-244">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ae69f-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae69f-245">Al hacer clic en el icono de LearnUpon en el panel de acceso, debería iniciar sesión automáticamente en su aplicación LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="ae69f-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="ae69f-246">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae69f-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae69f-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ae69f-247">Additional resources</span></span>

* [<span data-ttu-id="ae69f-248">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae69f-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae69f-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae69f-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

