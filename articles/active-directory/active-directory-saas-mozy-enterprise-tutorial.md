---
title: "Tutorial: Integración de Azure Active Directory con Mozy Enterprise | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="311e3-103">Tutorial: Integración de Azure Active Directory con Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="311e3-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="311e3-104">En este tutorial, aprenderá a integrar Mozy Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="311e3-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="311e3-105">La integración de Mozy Enterprise con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="311e3-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="311e3-106">Puede controlar en Azure AD quién tiene acceso a Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="311e3-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="311e3-107">Puede permitir que los usuarios inicien sesión automáticamente en Mozy Enterprise (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="311e3-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="311e3-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="311e3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="311e3-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="311e3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="311e3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="311e3-110">Prerequisites</span></span>

<span data-ttu-id="311e3-111">Para configurar la integración de Azure AD con Mozy Enterprise, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="311e3-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="311e3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="311e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="311e3-113">Una suscripción habilitada para el inicio de sesión único en Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="311e3-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="311e3-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="311e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="311e3-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="311e3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="311e3-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="311e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="311e3-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="311e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="311e3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="311e3-118">Scenario description</span></span>
<span data-ttu-id="311e3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="311e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="311e3-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="311e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="311e3-121">Adición de Mozy Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="311e3-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="311e3-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="311e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="311e3-123">Adición de Mozy Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="311e3-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="311e3-124">Para configurar la integración de Mozy Enterprise en Azure AD, es preciso agregar dicha solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="311e3-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="311e3-125">**Para agregar Mozy Enterprise desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="311e3-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="311e3-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="311e3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="311e3-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="311e3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="311e3-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="311e3-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="311e3-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="311e3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="311e3-133">En el cuadro de búsqueda, escriba **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="311e3-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="311e3-135">En el panel de resultados, seleccione **Mozy Enterprise** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="311e3-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="311e3-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="311e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="311e3-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mozy Enterprise con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="311e3-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="311e3-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Mozy Enterprise para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="311e3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="311e3-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="311e3-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="311e3-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="311e3-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="311e3-142">Para configurar y probar el inicio de sesión único de Azure AD con Mozy Enterprise, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="311e3-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="311e3-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="311e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="311e3-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="311e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="311e3-145">**[Creación de un usuario de prueba de Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**: el objetivo es tener un homólogo de Britta Simon en Mozy Enterprise que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="311e3-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="311e3-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="311e3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="311e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="311e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="311e3-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="311e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="311e3-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="311e3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="311e3-150">**Para configurar el inicio de sesión único de Azure AD con Mozy Enterprise, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="311e3-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="311e3-151">En la página de integración de la aplicación **Mozy Enterprise** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="311e3-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="311e3-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="311e3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="311e3-155">En la sección **Dominio y direcciones URL de Mozy Enterprise**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="311e3-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="311e3-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.Mozyenterprise.com`.</span><span class="sxs-lookup"><span data-stu-id="311e3-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="311e3-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="311e3-158">This value is not real.</span></span> <span data-ttu-id="311e3-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="311e3-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="311e3-160">Póngase en contacto con el [equipo de atención al cliente de Mozy Enterprise](http://support.mozy.com/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="311e3-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="311e3-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="311e3-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="311e3-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="311e3-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="311e3-165">En la sección **Configuración de Mozy Enterprise**, haga clic en **Configurar Mozy Enterprise** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="311e3-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="311e3-166">Copie **SAML Entity ID and SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML e Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="311e3-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="311e3-168">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="311e3-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="311e3-169">En la sección **Configuración**, haga clic en **Directiva de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="311e3-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="311e3-170">![Directiva de autenticación](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Directiva de autenticación")</span><span class="sxs-lookup"><span data-stu-id="311e3-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="311e3-171">En la sección **Authentication Policy** (Directiva de autenticación), realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="311e3-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="311e3-172">![Directiva de autenticación](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Directiva de autenticación")</span><span class="sxs-lookup"><span data-stu-id="311e3-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="311e3-173">a.</span><span class="sxs-lookup"><span data-stu-id="311e3-173">a.</span></span> <span data-ttu-id="311e3-174">Seleccione **Servicio de directorio** como **Proveedor**.</span><span class="sxs-lookup"><span data-stu-id="311e3-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="311e3-175">b.</span><span class="sxs-lookup"><span data-stu-id="311e3-175">b.</span></span> <span data-ttu-id="311e3-176">Seleccione **Use LDAP Push**(Usar inserción de LDAP).</span><span class="sxs-lookup"><span data-stu-id="311e3-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="311e3-177">c.</span><span class="sxs-lookup"><span data-stu-id="311e3-177">c.</span></span> <span data-ttu-id="311e3-178">Haga clic en la pestaña **Autenticación SAML** .</span><span class="sxs-lookup"><span data-stu-id="311e3-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="311e3-179">d.</span><span class="sxs-lookup"><span data-stu-id="311e3-179">d.</span></span> <span data-ttu-id="311e3-180">Pegue el valor de **dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal en el cuadro de texto **IdP Login URL** (Dirección URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="311e3-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="311e3-181">e.</span><span class="sxs-lookup"><span data-stu-id="311e3-181">e.</span></span> <span data-ttu-id="311e3-182">Pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **IdP Entity ID** (Identificador de entidad del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="311e3-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="311e3-183">f.</span><span class="sxs-lookup"><span data-stu-id="311e3-183">f.</span></span> <span data-ttu-id="311e3-184">Abra el certificado codificado en base 64 descargado en el Bloc de notas, copie su contenido en el Portapapeles y, a continuación, pegue todo el certificado en el cuadro de texto **Certificado SAML**.</span><span class="sxs-lookup"><span data-stu-id="311e3-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="311e3-185">g.</span><span class="sxs-lookup"><span data-stu-id="311e3-185">g.</span></span> <span data-ttu-id="311e3-186">Seleccione **Habilitar SSO para que los administradores inicien sesión con sus credenciales de red**.</span><span class="sxs-lookup"><span data-stu-id="311e3-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="311e3-187">h.</span><span class="sxs-lookup"><span data-stu-id="311e3-187">h.</span></span> <span data-ttu-id="311e3-188">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="311e3-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="311e3-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="311e3-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="311e3-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="311e3-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="311e3-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="311e3-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="311e3-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="311e3-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="311e3-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="311e3-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="311e3-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="311e3-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="311e3-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="311e3-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="311e3-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="311e3-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="311e3-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="311e3-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="311e3-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="311e3-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="311e3-204">a.</span><span class="sxs-lookup"><span data-stu-id="311e3-204">a.</span></span> <span data-ttu-id="311e3-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="311e3-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="311e3-206">b.</span><span class="sxs-lookup"><span data-stu-id="311e3-206">b.</span></span> <span data-ttu-id="311e3-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="311e3-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="311e3-208">c.</span><span class="sxs-lookup"><span data-stu-id="311e3-208">c.</span></span> <span data-ttu-id="311e3-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="311e3-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="311e3-210">d.</span><span class="sxs-lookup"><span data-stu-id="311e3-210">d.</span></span> <span data-ttu-id="311e3-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="311e3-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="311e3-212">Creación de un usuario de prueba de Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="311e3-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="311e3-213">Para permitir que los usuarios de Azure AD inicien sesión en Mozy Enterprise, deben aprovisionarse en Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="311e3-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="311e3-214">En el caso de Mozy Enterprise, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="311e3-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="311e3-215">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Mozy Enterprise ofrecida por Mozy Enterprise para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="311e3-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="311e3-216">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="311e3-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="311e3-217">Inicie sesión en su inquilino de **Mozy Enterprise** .</span><span class="sxs-lookup"><span data-stu-id="311e3-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="311e3-218">Haga clic en **Usuarios** y, luego, en **Agregar nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="311e3-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="311e3-219">![Usuarios](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="311e3-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="311e3-220">La opción **Agregar nuevo usuario** solo se muestra si **Mozy** está seleccionado como proveedor en **Directiva de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="311e3-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="311e3-221">Si la autenticación SAML está configurada, los usuarios se agregan automáticamente al iniciar sesión por primera vez con inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="311e3-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="311e3-222">En el cuadro de diálogo Nuevo usuario, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="311e3-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="311e3-223">![Agregar usuarios](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Agregar usuarios")</span><span class="sxs-lookup"><span data-stu-id="311e3-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="311e3-224">a.</span><span class="sxs-lookup"><span data-stu-id="311e3-224">a.</span></span> <span data-ttu-id="311e3-225">En la lista **Choose a Group** (Elija un grupo), seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="311e3-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="311e3-226">b.</span><span class="sxs-lookup"><span data-stu-id="311e3-226">b.</span></span> <span data-ttu-id="311e3-227">En la lista **Tipo de usuario** , seleccione un tipo.</span><span class="sxs-lookup"><span data-stu-id="311e3-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="311e3-228">c.</span><span class="sxs-lookup"><span data-stu-id="311e3-228">c.</span></span> <span data-ttu-id="311e3-229">En el cuadro de texto **Username** (Nombre de usuario), escriba el nombre de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="311e3-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="311e3-230">d.</span><span class="sxs-lookup"><span data-stu-id="311e3-230">d.</span></span> <span data-ttu-id="311e3-231">En el cuadro de texto **Email** (Correo electrónico), escriba la dirección de correo electrónico del usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="311e3-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="311e3-232">e.</span><span class="sxs-lookup"><span data-stu-id="311e3-232">e.</span></span> <span data-ttu-id="311e3-233">Seleccione **Send user instruction email**(Enviar correo electrónico al usuario con instrucciones).</span><span class="sxs-lookup"><span data-stu-id="311e3-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="311e3-234">f.</span><span class="sxs-lookup"><span data-stu-id="311e3-234">f.</span></span> <span data-ttu-id="311e3-235">Haga clic en **Add User(s)**(Agregar usuarios).</span><span class="sxs-lookup"><span data-stu-id="311e3-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="311e3-236">Después de crear el usuario, se enviará un correo electrónico al usuario de Azure AD que incluye un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="311e3-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="311e3-237">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="311e3-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="311e3-238">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="311e3-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="311e3-240">**Para asignar a Britta Simon a Mozy Enterprise, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="311e3-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="311e3-241">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="311e3-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="311e3-243">En la lista de aplicaciones, seleccione **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="311e3-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="311e3-245">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="311e3-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="311e3-247">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="311e3-247">Click **Add** button.</span></span> <span data-ttu-id="311e3-248">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="311e3-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="311e3-250">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="311e3-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="311e3-251">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="311e3-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="311e3-252">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="311e3-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="311e3-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="311e3-253">Testing single sign-on</span></span>

<span data-ttu-id="311e3-254">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="311e3-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="311e3-255">Al hacer clic en el icono de Mozy Enterprise en el Panel de acceso, debería entrar en la página de inicio de sesión de dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="311e3-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="311e3-256">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="311e3-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="311e3-257">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="311e3-257">Additional resources</span></span>

* [<span data-ttu-id="311e3-258">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="311e3-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="311e3-259">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="311e3-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

