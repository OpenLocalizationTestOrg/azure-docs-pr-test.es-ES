---
title: "Tutorial: Integración de Azure Active Directory con Kintone | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="f19be-103">Tutorial: Integración de Azure Active Directory con Kintone</span><span class="sxs-lookup"><span data-stu-id="f19be-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="f19be-104">En este tutorial, aprenderá a integrar Kintone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f19be-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f19be-105">La integración de Kintone con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f19be-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f19be-106">En Azure AD se puede controlar quién tiene acceso a Kintone</span><span class="sxs-lookup"><span data-stu-id="f19be-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="f19be-107">Puede permitir que los usuarios inicien sesión automáticamente en Kintone (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f19be-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f19be-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f19be-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f19be-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f19be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f19be-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f19be-110">Prerequisites</span></span>

<span data-ttu-id="f19be-111">Para configurar la integración de Azure AD con Kintone, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f19be-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="f19be-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f19be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f19be-113">Una suscripción habilitada para inicio de sesión único en Kintone</span><span class="sxs-lookup"><span data-stu-id="f19be-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f19be-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f19be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f19be-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f19be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f19be-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f19be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f19be-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f19be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f19be-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f19be-118">Scenario description</span></span>
<span data-ttu-id="f19be-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f19be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f19be-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f19be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f19be-121">Adición de Kintone desde la galería</span><span class="sxs-lookup"><span data-stu-id="f19be-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="f19be-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f19be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="f19be-123">Adición de Kintone desde la galería</span><span class="sxs-lookup"><span data-stu-id="f19be-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="f19be-124">Para configurar la integración de Kintone en Azure AD, deberá agregar Kintone desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f19be-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f19be-125">**Para agregar Kintone desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f19be-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f19be-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f19be-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f19be-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f19be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f19be-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f19be-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f19be-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f19be-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f19be-133">En el cuadro de búsqueda, escriba **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="f19be-133">In the search box, type **Kintone**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="f19be-135">En el panel de resultados, seleccione **Kintone** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f19be-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f19be-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f19be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f19be-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kintone con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f19be-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f19be-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Kintone para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f19be-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="f19be-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Kintone.</span><span class="sxs-lookup"><span data-stu-id="f19be-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="f19be-141">Para establecer la relación de vínculo, en Kintone, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f19be-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f19be-142">Para configurar y probar el inicio de sesión único de Azure AD con Kintone, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f19be-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f19be-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f19be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f19be-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f19be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f19be-145">**[Creación de un usuario de prueba de Kintone](#creating-a-kintone-test-user)**: para tener un homólogo de Britta Simon en Kintone que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="f19be-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f19be-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f19be-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f19be-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f19be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f19be-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f19be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f19be-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en Kintone.</span><span class="sxs-lookup"><span data-stu-id="f19be-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="f19be-150">**Para configurar el inicio de sesión único de Azure AD con Kintone, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f19be-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="f19be-151">En Azure Portal, en la página de integración de la aplicación **Kintone**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f19be-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f19be-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f19be-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="f19be-155">En la sección **Dominio y direcciones URL de Kintone**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f19be-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="f19be-157">a.</span><span class="sxs-lookup"><span data-stu-id="f19be-157">a.</span></span> <span data-ttu-id="f19be-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.kintone.com`.</span><span class="sxs-lookup"><span data-stu-id="f19be-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="f19be-159">b.</span><span class="sxs-lookup"><span data-stu-id="f19be-159">b.</span></span> <span data-ttu-id="f19be-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="f19be-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="f19be-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="f19be-161">These values are not real.</span></span> <span data-ttu-id="f19be-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f19be-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f19be-163">Póngase en contacto con el [equipo de soporte de cliente de Kintone](https://www.kintone.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="f19be-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="f19be-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f19be-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="f19be-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f19be-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f19be-168">En la sección **Configuración de Kintone**, haga clic en **Configurar Kintone** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f19be-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f19be-169">Copie los valores de **Dirección URL de cierre de sesión y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** de la **sección Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="f19be-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="f19be-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de **Kintone** .</span><span class="sxs-lookup"><span data-stu-id="f19be-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="f19be-172">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="f19be-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="f19be-173">![Configuración](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="f19be-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="f19be-174">Haga clic en **Users & System Administration** (Administración del sistema y usuarios).</span><span class="sxs-lookup"><span data-stu-id="f19be-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="f19be-175">![Administración de usuarios y del sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administración de usuarios y del sistema")</span><span class="sxs-lookup"><span data-stu-id="f19be-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="f19be-176">En **Administración del sistema \> Seguridad**, haga clic en **Inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f19be-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="f19be-177">![Inicio de sesión](./media/active-directory-saas-kintone-tutorial/ic785881.png "inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="f19be-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="f19be-178">Haga clic en **Habilitar autenticación SAML**.</span><span class="sxs-lookup"><span data-stu-id="f19be-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="f19be-179">![Autenticación SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="f19be-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="f19be-180">En la sección SAML Authentication (Autenticación SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f19be-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="f19be-181">![Autenticación SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="f19be-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="f19be-182">a.</span><span class="sxs-lookup"><span data-stu-id="f19be-182">a.</span></span> <span data-ttu-id="f19be-183">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL de inicio de sesión de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f19be-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f19be-184">b.</span><span class="sxs-lookup"><span data-stu-id="f19be-184">b.</span></span> <span data-ttu-id="f19be-185">En el cuadro de texto **Dirección URL de cierre de sesión**, pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f19be-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f19be-186">c.</span><span class="sxs-lookup"><span data-stu-id="f19be-186">c.</span></span> <span data-ttu-id="f19be-187">Haga clic en **Browse** (Examinar) para cargar el certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="f19be-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="f19be-188">d.</span><span class="sxs-lookup"><span data-stu-id="f19be-188">d.</span></span> <span data-ttu-id="f19be-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f19be-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f19be-190">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f19be-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f19be-191">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f19be-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f19be-192">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f19be-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f19be-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f19be-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="f19be-194">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f19be-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f19be-196">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f19be-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f19be-197">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f19be-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f19be-199">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f19be-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f19be-201">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f19be-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f19be-203">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f19be-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f19be-205">a.</span><span class="sxs-lookup"><span data-stu-id="f19be-205">a.</span></span> <span data-ttu-id="f19be-206">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f19be-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f19be-207">b.</span><span class="sxs-lookup"><span data-stu-id="f19be-207">b.</span></span> <span data-ttu-id="f19be-208">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f19be-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f19be-209">c.</span><span class="sxs-lookup"><span data-stu-id="f19be-209">c.</span></span> <span data-ttu-id="f19be-210">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f19be-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f19be-211">d.</span><span class="sxs-lookup"><span data-stu-id="f19be-211">d.</span></span> <span data-ttu-id="f19be-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f19be-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="f19be-213">Creación de un usuario de prueba de Kintone</span><span class="sxs-lookup"><span data-stu-id="f19be-213">Creating a Kintone test user</span></span>

<span data-ttu-id="f19be-214">Para permitir que los usuarios de Azure AD inicien sesión en Kintone, deben aprovisionarse en Kintone.</span><span class="sxs-lookup"><span data-stu-id="f19be-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="f19be-215">En el caso de Kintone, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="f19be-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="f19be-216">Para aprovisionar una cuenta de usuario, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f19be-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="f19be-217">Inicie sesión en el sitio de la compañía de **Kintone** como administrador.</span><span class="sxs-lookup"><span data-stu-id="f19be-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="f19be-218">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="f19be-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="f19be-219">![Configuración](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="f19be-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="f19be-220">Haga clic en **Users & System Administration** (Administración del sistema y usuarios).</span><span class="sxs-lookup"><span data-stu-id="f19be-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="f19be-221">![Administración de usuarios y del sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administración de usuarios y del sistema")</span><span class="sxs-lookup"><span data-stu-id="f19be-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="f19be-222">En **Administración de usuarios** haga clic en **Departamentos y usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f19be-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="f19be-223">![Departamentos y usuarios](./media/active-directory-saas-kintone-tutorial/ic785888.png "Departamentos y usuarios")</span><span class="sxs-lookup"><span data-stu-id="f19be-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="f19be-224">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="f19be-224">Click **New User**.</span></span>
   
    <span data-ttu-id="f19be-225">![Nuevos usuarios](./media/active-directory-saas-kintone-tutorial/ic785889.png "Nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="f19be-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="f19be-226">En la sección **Nuevo usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f19be-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f19be-227">![Nuevos usuarios](./media/active-directory-saas-kintone-tutorial/ic785890.png "Nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="f19be-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="f19be-228">a.</span><span class="sxs-lookup"><span data-stu-id="f19be-228">a.</span></span> <span data-ttu-id="f19be-229">Escriba un **Nombre para mostrar**, **Nombre de inicio de sesión**, **Nueva contraseña**, **Confirmar contraseña**, **Dirección de correo electrónico** y otros detalles de una cuenta válida de AAD que quiera aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="f19be-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="f19be-230">b.</span><span class="sxs-lookup"><span data-stu-id="f19be-230">b.</span></span> <span data-ttu-id="f19be-231">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f19be-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="f19be-232">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Kintone ofrecida por Kintone para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="f19be-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f19be-233">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f19be-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f19be-234">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Kintone.</span><span class="sxs-lookup"><span data-stu-id="f19be-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f19be-236">**Para asignar a Britta Simon a Kintone, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="f19be-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="f19be-237">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f19be-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f19be-239">En la lista de aplicaciones, seleccione **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="f19be-239">In the applications list, select **Kintone**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="f19be-241">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f19be-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f19be-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f19be-243">Click **Add** button.</span></span> <span data-ttu-id="f19be-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f19be-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f19be-246">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f19be-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f19be-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f19be-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f19be-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f19be-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f19be-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f19be-249">Testing single sign-on</span></span>

<span data-ttu-id="f19be-250">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f19be-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f19be-251">Al hacer clic en el icono de Kintone en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Kintone.</span><span class="sxs-lookup"><span data-stu-id="f19be-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f19be-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f19be-252">Additional resources</span></span>

* [<span data-ttu-id="f19be-253">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f19be-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f19be-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f19be-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

