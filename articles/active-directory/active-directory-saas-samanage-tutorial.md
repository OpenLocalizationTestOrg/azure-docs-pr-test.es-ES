---
title: "Tutorial: integración de Azure Active Directory con Samanage | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c54dbe407145a29a712acc3c0fb549a38ac26bed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="7791d-103">Tutorial: integración de Azure Active Directory con Samanage</span><span class="sxs-lookup"><span data-stu-id="7791d-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="7791d-104">En este tutorial, obtendrá información sobre cómo integrar Samanage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7791d-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7791d-105">La integración de Samanage con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7791d-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7791d-106">Puede controlar en Azure AD quién tiene acceso a Samanage.</span><span class="sxs-lookup"><span data-stu-id="7791d-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="7791d-107">Puede habilitar que los usuarios inicien sesión automáticamente en Samanage (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7791d-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7791d-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7791d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7791d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7791d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7791d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7791d-110">Prerequisites</span></span>

<span data-ttu-id="7791d-111">Para configurar la integración de Azure AD con Samanage, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7791d-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="7791d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7791d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7791d-113">Una suscripción habilitada para el inicio de sesión único en Samanage</span><span class="sxs-lookup"><span data-stu-id="7791d-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7791d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7791d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7791d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7791d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7791d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7791d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7791d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7791d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7791d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7791d-118">Scenario description</span></span>
<span data-ttu-id="7791d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7791d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7791d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="7791d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7791d-121">Adición de Samanage desde la galería</span><span class="sxs-lookup"><span data-stu-id="7791d-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="7791d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7791d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="7791d-123">Adición de Samanage desde la galería</span><span class="sxs-lookup"><span data-stu-id="7791d-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="7791d-124">Para configurar la integración de Samanage en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="7791d-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7791d-125">**Para agregar Samanage desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="7791d-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7791d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7791d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7791d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7791d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7791d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7791d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7791d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7791d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7791d-133">En el cuadro de búsqueda, escriba **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="7791d-133">In the search box, type **Samanage**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="7791d-135">En el panel de resultados, seleccione **Samanage** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7791d-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7791d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7791d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7791d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Samanage con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7791d-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7791d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Samanage para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7791d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="7791d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Samanage.</span><span class="sxs-lookup"><span data-stu-id="7791d-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="7791d-141">Para establecer la relación de vínculo, en Samanage, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7791d-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7791d-142">Para configurar y probar el inicio de sesión único de Azure AD con Samanage, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7791d-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7791d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="7791d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7791d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7791d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7791d-145">**[Creación de un usuario de prueba en Samanage](#creating-a-samanage-test-user)**: para tener un homólogo de Britta Simon en Samanage que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7791d-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7791d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7791d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7791d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7791d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7791d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7791d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7791d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Samanage.</span><span class="sxs-lookup"><span data-stu-id="7791d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="7791d-150">**Para configurar el inicio de sesión único de Azure AD con Samanage, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="7791d-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="7791d-151">En Azure Portal, en la página de integración de la aplicación **Samanage**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7791d-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7791d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7791d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="7791d-155">En la sección **Dominio y direcciones URL de Samanage**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7791d-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="7791d-157">a.</span><span class="sxs-lookup"><span data-stu-id="7791d-157">a.</span></span> <span data-ttu-id="7791d-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<Company Name>.samanage.com/saml_login/<Company Name>`.</span><span class="sxs-lookup"><span data-stu-id="7791d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="7791d-159">b.</span><span class="sxs-lookup"><span data-stu-id="7791d-159">b.</span></span> <span data-ttu-id="7791d-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="7791d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7791d-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7791d-161">These values are not real.</span></span> <span data-ttu-id="7791d-162">Actualice estos valores con la dirección URL de inicio de sesión y el identificador reales, que se explican más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="7791d-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="7791d-163">Para más información, póngase en contacto con [equipo de soporte al cliente de Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="7791d-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="7791d-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7791d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="7791d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7791d-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7791d-168">En la sección **Configuración de Samanage**, haga clic en **Configurar Samanage** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="7791d-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7791d-169">Copie los valores de **Sign-Out URL (Dirección URL de cierre de sesión) y SAML Entity ID (Identificador de entidad de SAML)** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="7791d-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="7791d-171">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Samanage como administrador.</span><span class="sxs-lookup"><span data-stu-id="7791d-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="7791d-172">Haga clic en **Dashboard** (Panel) y seleccione **Setup** (Configuración) en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="7791d-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="7791d-173">![Panel](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Panel")</span><span class="sxs-lookup"><span data-stu-id="7791d-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="7791d-174">Haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7791d-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="7791d-175">![Inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="7791d-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="7791d-176">Navegue hasta la sección **Login using SAML** (Iniciar sesión con SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7791d-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="7791d-177">![Inicio de sesión con SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Inicio de sesión con SAML")</span><span class="sxs-lookup"><span data-stu-id="7791d-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="7791d-178">a.</span><span class="sxs-lookup"><span data-stu-id="7791d-178">a.</span></span> <span data-ttu-id="7791d-179">Haga clic en **Enable Single Sign-On with SAML**(Habilitar inicio de sesión único con SAML).</span><span class="sxs-lookup"><span data-stu-id="7791d-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="7791d-180">b.</span><span class="sxs-lookup"><span data-stu-id="7791d-180">b.</span></span> <span data-ttu-id="7791d-181">En el cuadro de texto **Identity provider URL** (Dirección URL del proveedor de identidad), pegue el valor del **identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7791d-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="7791d-182">c.</span><span class="sxs-lookup"><span data-stu-id="7791d-182">c.</span></span> <span data-ttu-id="7791d-183">Confirme que la **dirección URL de inicio de sesión** coincide con la **dirección URL de inicio de sesión** de la sección **Dominio y direcciones URL de Samanage**  en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7791d-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="7791d-184">d.</span><span class="sxs-lookup"><span data-stu-id="7791d-184">d.</span></span> <span data-ttu-id="7791d-185">En el cuadro de texto **Logout URL** (Dirección URL de cierre de sesión), pegue el valor de la **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7791d-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="7791d-186">e.</span><span class="sxs-lookup"><span data-stu-id="7791d-186">e.</span></span> <span data-ttu-id="7791d-187">En el cuadro de texto **SAML Issuer** (Emisor de SAML) escriba el URI del identificador de la aplicación establecido en el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="7791d-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="7791d-188">f.</span><span class="sxs-lookup"><span data-stu-id="7791d-188">f.</span></span> <span data-ttu-id="7791d-189">En el Bloc de notas, abra el certificado codificado en base 64 descargado de Azure Portal, copie su contenido en el Portapapeles y péguelo en el cuadro de texto **Paste your Identity Provider x.509 Certificate below** (Pegue a continuación el certificado x.509 del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="7791d-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="7791d-190">g.</span><span class="sxs-lookup"><span data-stu-id="7791d-190">g.</span></span> <span data-ttu-id="7791d-191">Haga clic en **Create users if they do not exist in Samanage**(Crear usuarios si no existen en Samanage).</span><span class="sxs-lookup"><span data-stu-id="7791d-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="7791d-192">h.</span><span class="sxs-lookup"><span data-stu-id="7791d-192">h.</span></span> <span data-ttu-id="7791d-193">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="7791d-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="7791d-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7791d-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7791d-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7791d-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7791d-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7791d-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7791d-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7791d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="7791d-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7791d-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7791d-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="7791d-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7791d-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7791d-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7791d-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7791d-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7791d-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7791d-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7791d-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7791d-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7791d-209">a.</span><span class="sxs-lookup"><span data-stu-id="7791d-209">a.</span></span> <span data-ttu-id="7791d-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7791d-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7791d-211">b.</span><span class="sxs-lookup"><span data-stu-id="7791d-211">b.</span></span> <span data-ttu-id="7791d-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7791d-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7791d-213">c.</span><span class="sxs-lookup"><span data-stu-id="7791d-213">c.</span></span> <span data-ttu-id="7791d-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7791d-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7791d-215">d.</span><span class="sxs-lookup"><span data-stu-id="7791d-215">d.</span></span> <span data-ttu-id="7791d-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7791d-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="7791d-217">Creación de un usuario de prueba en Samanage</span><span class="sxs-lookup"><span data-stu-id="7791d-217">Creating a Samanage test user</span></span>

<span data-ttu-id="7791d-218">Para permitir que los usuarios de Azure AD inicien sesión en Samanage, tienen que aprovisionarse en Samanage.</span><span class="sxs-lookup"><span data-stu-id="7791d-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="7791d-219">En el caso de Samanage, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="7791d-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="7791d-220">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="7791d-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7791d-221">Inicie sesión en su sitio de la compañía de Samanage como administrador.</span><span class="sxs-lookup"><span data-stu-id="7791d-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="7791d-222">Haga clic en **Dashboard** (Panel) y seleccione **Setup** (Configuración) en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="7791d-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="7791d-223">![Instalación](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="7791d-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="7791d-224">Haga clic en la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="7791d-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="7791d-225">![Usuarios](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="7791d-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="7791d-226">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="7791d-226">Click **New User**.</span></span>
   
    <span data-ttu-id="7791d-227">![Nuevo usuario](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="7791d-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="7791d-228">Escriba el **nombre** y la **dirección de correo electrónico** de la cuenta de Azure Active Directory que desea aprovisionar y haga clic en **Create user** (Crear usuario).</span><span class="sxs-lookup"><span data-stu-id="7791d-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="7791d-229">![Creación de usuarios](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="7791d-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="7791d-230">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="7791d-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="7791d-231">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Samanage que proporcione Samanage para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7791d-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7791d-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7791d-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7791d-233">En esta sección, concederá acceso a Britta Simon a Samanage para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="7791d-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7791d-235">**Para asignar a Britta Simon a Samanage, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="7791d-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="7791d-236">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7791d-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7791d-238">En la lista de aplicaciones, seleccione **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="7791d-238">In the applications list, select **Samanage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="7791d-240">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7791d-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7791d-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7791d-242">Click **Add** button.</span></span> <span data-ttu-id="7791d-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7791d-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7791d-245">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7791d-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7791d-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7791d-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7791d-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7791d-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7791d-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7791d-248">Testing single sign-on</span></span>

<span data-ttu-id="7791d-249">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7791d-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7791d-250">Al hacer clic en el icono de Samanage en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Samanage.</span><span class="sxs-lookup"><span data-stu-id="7791d-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="7791d-251">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7791d-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7791d-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7791d-252">Additional resources</span></span>

* [<span data-ttu-id="7791d-253">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7791d-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7791d-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7791d-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

