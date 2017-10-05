---
title: "Tutorial: Integración de Azure Active Directory con Promapp | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="7ff8d-103">Tutorial: Integración de Azure Active Directory con Promapp</span><span class="sxs-lookup"><span data-stu-id="7ff8d-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="7ff8d-104">En este tutorial, obtendrá información sobre cómo integrar Promapp con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ff8d-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ff8d-105">Integrar Promapp con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ff8d-106">Puede controlar en Azure AD quién tiene acceso a Promapp.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="7ff8d-107">Puede permitir que los usuarios inicien sesión automáticamente en Promapp (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ff8d-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ff8d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ff8d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ff8d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7ff8d-110">Prerequisites</span></span>

<span data-ttu-id="7ff8d-111">Para configurar la integración de Azure AD con Promapp, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="7ff8d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ff8d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ff8d-113">Una suscripción habilitada para el inicio de sesión único en Promapp</span><span class="sxs-lookup"><span data-stu-id="7ff8d-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ff8d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ff8d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ff8d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ff8d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ff8d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ff8d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7ff8d-118">Scenario description</span></span>
<span data-ttu-id="7ff8d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ff8d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ff8d-121">Incorporación de Promapp desde la galería</span><span class="sxs-lookup"><span data-stu-id="7ff8d-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="7ff8d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ff8d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="7ff8d-123">Incorporación de Promapp desde la galería</span><span class="sxs-lookup"><span data-stu-id="7ff8d-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="7ff8d-124">Para configurar la integración de Promapp en Azure AD, deberá agregar Promapp desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ff8d-125">**Para agregar Promapp desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7ff8d-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff8d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ff8d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ff8d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7ff8d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7ff8d-133">En el cuadro de búsqueda, escriba **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-133">In the search box, type **Promapp**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="7ff8d-135">En el panel de resultados, seleccione **Promapp** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ff8d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ff8d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ff8d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Promapp con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7ff8d-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ff8d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Promapp para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="7ff8d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Promapp.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="7ff8d-141">Para establecer la relación de vínculo, en Promapp, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7ff8d-142">Para configurar y probar el inicio de sesión único de Azure AD con Promapp, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ff8d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ff8d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ff8d-145">**[Creación de un usuario de prueba de Promapp](#creating-a-promapp-test-user)**: Para tener un homólogo de Britta Simon en Promapp que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ff8d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ff8d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ff8d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ff8d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ff8d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Promapp.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="7ff8d-150">**Para configurar el inicio de sesión único de Azure AD con Promapp, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7ff8d-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff8d-151">En Azure Portal, en la página de integración de la aplicación **Promapp**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7ff8d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="7ff8d-155">En la sección **Dominio y direcciones URL de Promapp**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="7ff8d-157">a.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-157">a.</span></span> <span data-ttu-id="7ff8d-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="7ff8d-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-159">b.</span></span> <span data-ttu-id="7ff8d-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="7ff8d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ff8d-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-161">These values are not real.</span></span> <span data-ttu-id="7ff8d-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7ff8d-163">Póngase en contacto con el [equipo de soporte técnico de Promapp](https://www.promapp.com/about-us/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="7ff8d-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="7ff8d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7ff8d-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ff8d-168">En la sección **Configuración de Promapp**, haga clic en **Configurar Promapp** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ff8d-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="7ff8d-171">Inicie sesión en su sitio de la empresa Promapp como administrador.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="7ff8d-172">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Inicio de sesión único de Azure AD][12]

9. <span data-ttu-id="7ff8d-174">Haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-174">Click **Configure**.</span></span> 
   
    ![Inicio de sesión único de Azure AD][13]

10. <span data-ttu-id="7ff8d-176">En la pestaña **Seguridad** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Inicio de sesión único de Azure AD][14]
    
    <span data-ttu-id="7ff8d-178">a.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-178">a.</span></span> <span data-ttu-id="7ff8d-179">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal en el cuadro de texto **SSO-Login URL** (Dirección URL de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="7ff8d-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="7ff8d-180">b.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-180">b.</span></span> <span data-ttu-id="7ff8d-181">En **SSO - Single Sign-on Mode** (SSO - Modo de inicio de sesión único), seleccione **Optional** (Opcional) y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="7ff8d-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="7ff8d-182">c.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-182">c.</span></span> <span data-ttu-id="7ff8d-183">Abra el certificado descargado en el Bloc de notas, copie el contenido del certificado sin la primera línea (-----BEGIN CERTIFICATE-----) ni la última (-----END CERTIFICATE-----), péguelo en el cuadro de texto **Certificado X.509 de inicio de sesión único** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="7ff8d-184">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ff8d-185">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ff8d-186">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ff8d-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ff8d-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ff8d-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ff8d-188">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7ff8d-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7ff8d-190">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="7ff8d-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff8d-191">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ff8d-193">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ff8d-195">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ff8d-197">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7ff8d-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ff8d-199">a.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-199">a.</span></span> <span data-ttu-id="7ff8d-200">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ff8d-201">b.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-201">b.</span></span> <span data-ttu-id="7ff8d-202">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ff8d-203">c.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-203">c.</span></span> <span data-ttu-id="7ff8d-204">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ff8d-205">d.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-205">d.</span></span> <span data-ttu-id="7ff8d-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="7ff8d-207">Creación de un usuario de prueba de Promapp</span><span class="sxs-lookup"><span data-stu-id="7ff8d-207">Creating a Promapp test user</span></span>

<span data-ttu-id="7ff8d-208">La aplicación Promapp admite aprovisionamiento Just-in-Time.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="7ff8d-209">Esto significa que, si es necesario, se crea automáticamente una cuenta de usuario durante un intento de acceso a la aplicación mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ff8d-210">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ff8d-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ff8d-211">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Promapp.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7ff8d-213">**Para asignar a Britta Simon a Promapp, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7ff8d-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff8d-214">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7ff8d-216">En la lista de aplicaciones, seleccione **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-216">In the applications list, select **Promapp**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="7ff8d-218">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7ff8d-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-220">Click **Add** button.</span></span> <span data-ttu-id="7ff8d-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7ff8d-223">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ff8d-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ff8d-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ff8d-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7ff8d-226">Testing single sign-on</span></span>

<span data-ttu-id="7ff8d-227">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7ff8d-228">Al hacer clic en el icono de Promapp en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Promapp.</span><span class="sxs-lookup"><span data-stu-id="7ff8d-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ff8d-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7ff8d-229">Additional resources</span></span>

* [<span data-ttu-id="7ff8d-230">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ff8d-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ff8d-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ff8d-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

