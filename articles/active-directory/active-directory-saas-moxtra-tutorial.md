---
title: "Tutorial: Integración de Azure Active Directory con Moxtra | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="524af-103">Tutorial: Integración de Azure Active Directory con Moxtra</span><span class="sxs-lookup"><span data-stu-id="524af-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="524af-104">En este tutorial, obtendrá información sobre cómo integrar Moxtra con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="524af-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="524af-105">Integrar Moxtra con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="524af-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="524af-106">Puede controlar en Azure AD quién tiene acceso a Moxtra.</span><span class="sxs-lookup"><span data-stu-id="524af-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="524af-107">Puede permitir que los usuarios inicien sesión automáticamente en Moxtra (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="524af-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="524af-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="524af-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="524af-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="524af-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="524af-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="524af-110">Prerequisites</span></span>

<span data-ttu-id="524af-111">Para configurar la integración de Azure AD con Moxtra, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="524af-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="524af-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="524af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="524af-113">Una suscripción habilitada para el inicio de sesión único en Moxtra</span><span class="sxs-lookup"><span data-stu-id="524af-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="524af-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="524af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="524af-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="524af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="524af-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="524af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="524af-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="524af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="524af-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="524af-118">Scenario description</span></span>
<span data-ttu-id="524af-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="524af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="524af-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="524af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="524af-121">Incorporación de Moxtra desde la galería</span><span class="sxs-lookup"><span data-stu-id="524af-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="524af-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="524af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="524af-123">Incorporación de Moxtra desde la galería</span><span class="sxs-lookup"><span data-stu-id="524af-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="524af-124">Para configurar la integración de Moxtra en Azure AD, es preciso agregar Moxtra desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="524af-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="524af-125">**Para agregar Moxtra desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="524af-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="524af-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="524af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="524af-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="524af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="524af-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="524af-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="524af-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="524af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="524af-133">En el cuadro de búsqueda, escriba **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="524af-133">In the search box, type **Moxtra**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="524af-135">En el panel de resultados, seleccione **Moxtra** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="524af-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="524af-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="524af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="524af-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Moxtra con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="524af-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="524af-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Moxtra para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="524af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="524af-140">Es decir, hay que establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Moxtra.</span><span class="sxs-lookup"><span data-stu-id="524af-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="524af-141">Para establecer la relación de vínculo, en Moxtra, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="524af-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="524af-142">Para configurar y probar el inicio de sesión único de Azure AD con Moxtra, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="524af-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="524af-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="524af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="524af-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="524af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="524af-145">**[Creación de un usuario de prueba de Moxtra](#creating-a-moxtra-test-user)**: para tener un homólogo de Britta Simon en Moxtra que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="524af-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="524af-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="524af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="524af-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="524af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="524af-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="524af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="524af-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Moxtra.</span><span class="sxs-lookup"><span data-stu-id="524af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="524af-150">**Para configurar el inicio de sesión único de Azure AD con Moxtra, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="524af-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="524af-151">En Azure Portal, en la página de integración de la aplicación **Moxtra**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="524af-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="524af-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="524af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="524af-155">En la sección **Dominio y direcciones URL de Moxtra**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="524af-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="524af-157">En el cuadro de texto **URL de inicio de sesión**, escriba una URL como: `https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="524af-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="524af-158">La aplicación Moxtra espera las aserciones de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="524af-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="524af-159">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="524af-159">Configure the following claims for this application.</span></span> <span data-ttu-id="524af-160">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="524af-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="524af-161">En la siguiente captura de pantalla se muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="524af-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="524af-163">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="524af-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="524af-164">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="524af-164">Attribute Name</span></span> | <span data-ttu-id="524af-165">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="524af-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="524af-166">firstname</span><span class="sxs-lookup"><span data-stu-id="524af-166">firstname</span></span> | <span data-ttu-id="524af-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="524af-167">user.givenname</span></span> |
    | <span data-ttu-id="524af-168">lastname</span><span class="sxs-lookup"><span data-stu-id="524af-168">lastname</span></span> | <span data-ttu-id="524af-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="524af-169">user.surname</span></span> |
    | <span data-ttu-id="524af-170">idpid</span><span class="sxs-lookup"><span data-stu-id="524af-170">idpid</span></span>    | <span data-ttu-id="524af-171">< SAML Entity ID ></span><span class="sxs-lookup"><span data-stu-id="524af-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="524af-172">El valor del atributo **idpid** no es real.</span><span class="sxs-lookup"><span data-stu-id="524af-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="524af-173">Puede obtener el valor real de la sección **Quick reference** (Referencia rápida) en **Moxtra Configuration** (Configuración de Moxtra).</span><span class="sxs-lookup"><span data-stu-id="524af-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="524af-174">a.</span><span class="sxs-lookup"><span data-stu-id="524af-174">a.</span></span> <span data-ttu-id="524af-175">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="524af-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="524af-177">b.</span><span class="sxs-lookup"><span data-stu-id="524af-177">b.</span></span> <span data-ttu-id="524af-178">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="524af-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="524af-180">c.</span><span class="sxs-lookup"><span data-stu-id="524af-180">c.</span></span> <span data-ttu-id="524af-181">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="524af-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="524af-182">d.</span><span class="sxs-lookup"><span data-stu-id="524af-182">d.</span></span> <span data-ttu-id="524af-183">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="524af-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="524af-184">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="524af-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="524af-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="524af-186">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="524af-188">En la sección **Configuración de Moxtra**, haga clic en **Configurar Moxtra** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="524af-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="524af-189">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="524af-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="524af-191">En otra ventana del explorador, inicie sesión en su sitio de la compañía de Moxtra como administrador.</span><span class="sxs-lookup"><span data-stu-id="524af-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="524af-192">En la barra de herramientas de la izquierda, haga clic en **Admin Console > SAML Single Sign-on** (Consola de administración > Inicio de sesión único de SAML) y, luego, en **New** (Nuevo).</span><span class="sxs-lookup"><span data-stu-id="524af-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="524af-194">En la página **SAML** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="524af-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="524af-196">a.</span><span class="sxs-lookup"><span data-stu-id="524af-196">a.</span></span> <span data-ttu-id="524af-197">En el cuadro de texto **Nombre** , escriba el nombre de la configuración (por ejemplo, *SAML*).</span><span class="sxs-lookup"><span data-stu-id="524af-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="524af-198">b.</span><span class="sxs-lookup"><span data-stu-id="524af-198">b.</span></span> <span data-ttu-id="524af-199">En el cuadro de texto **IdP Entity ID** (Id. de entidad IdP), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="524af-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="524af-200">c.</span><span class="sxs-lookup"><span data-stu-id="524af-200">c.</span></span> <span data-ttu-id="524af-201">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="524af-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="524af-202">d.</span><span class="sxs-lookup"><span data-stu-id="524af-202">d.</span></span> <span data-ttu-id="524af-203">En el cuadro de texto **AuthnContextClassRef**, escriba **urn: oasis: nombres: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="524af-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="524af-204">e.</span><span class="sxs-lookup"><span data-stu-id="524af-204">e.</span></span> <span data-ttu-id="524af-205">En el cuadro de texto **NameID format** (Formato de id. de nombre), escriba **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="524af-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="524af-206">f.</span><span class="sxs-lookup"><span data-stu-id="524af-206">f.</span></span> <span data-ttu-id="524af-207">Abra el certificado que ha descargado desde Azure Portal en el Bloc de notas, copie el contenido y luego péguelo en el cuadro de texto **Certificate** (Certificado).</span><span class="sxs-lookup"><span data-stu-id="524af-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="524af-208">g.</span><span class="sxs-lookup"><span data-stu-id="524af-208">g.</span></span> <span data-ttu-id="524af-209">En el cuadro de texto del dominio de correo electrónico SAML, escriba su dominio de correo electrónico SAML.</span><span class="sxs-lookup"><span data-stu-id="524af-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="524af-210">Para ver los pasos para comprobar el dominio, haga clic en la "**i**" a continuación.</span><span class="sxs-lookup"><span data-stu-id="524af-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="524af-211">h.</span><span class="sxs-lookup"><span data-stu-id="524af-211">h.</span></span> <span data-ttu-id="524af-212">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="524af-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="524af-213">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="524af-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="524af-214">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="524af-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="524af-215">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="524af-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="524af-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="524af-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="524af-217">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="524af-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="524af-219">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="524af-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="524af-220">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="524af-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="524af-222">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="524af-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="524af-224">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="524af-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="524af-226">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="524af-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="524af-228">a.</span><span class="sxs-lookup"><span data-stu-id="524af-228">a.</span></span> <span data-ttu-id="524af-229">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="524af-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="524af-230">b.</span><span class="sxs-lookup"><span data-stu-id="524af-230">b.</span></span> <span data-ttu-id="524af-231">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="524af-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="524af-232">c.</span><span class="sxs-lookup"><span data-stu-id="524af-232">c.</span></span> <span data-ttu-id="524af-233">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="524af-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="524af-234">d.</span><span class="sxs-lookup"><span data-stu-id="524af-234">d.</span></span> <span data-ttu-id="524af-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="524af-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="524af-236">Creación de un usuario de prueba de Moxtra</span><span class="sxs-lookup"><span data-stu-id="524af-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="524af-237">El objetivo de esta sección es crear un usuario llamado Britta Simon en Moxtra.</span><span class="sxs-lookup"><span data-stu-id="524af-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="524af-238">**Para crear un usuario llamado Britta Simon en Moxtra, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="524af-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="524af-239">Inicie sesión en su sitio de la compañía de Moxtra como administrador.</span><span class="sxs-lookup"><span data-stu-id="524af-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="524af-240">En la barra de herramientas de la izquierda, haga clic en **Consola de administración > Administración de usuarios** y, luego, en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="524af-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="524af-242">En el cuadro de diálogo **Agregar usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="524af-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="524af-243">a.</span><span class="sxs-lookup"><span data-stu-id="524af-243">a.</span></span> <span data-ttu-id="524af-244">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="524af-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="524af-245">b.</span><span class="sxs-lookup"><span data-stu-id="524af-245">b.</span></span> <span data-ttu-id="524af-246">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="524af-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="524af-247">c.</span><span class="sxs-lookup"><span data-stu-id="524af-247">c.</span></span> <span data-ttu-id="524af-248">En el cuadro de texto **Email** (Correo electrónico), escriba la dirección de correo electrónico de Britta en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="524af-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="524af-249">d.</span><span class="sxs-lookup"><span data-stu-id="524af-249">d.</span></span> <span data-ttu-id="524af-250">En el cuadro de texto **Division** (División), escriba **Dev**.</span><span class="sxs-lookup"><span data-stu-id="524af-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="524af-251">e.</span><span class="sxs-lookup"><span data-stu-id="524af-251">e.</span></span> <span data-ttu-id="524af-252">En el cuadro de texto **Department** (Departamento), escriba **IT**.</span><span class="sxs-lookup"><span data-stu-id="524af-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="524af-253">f.</span><span class="sxs-lookup"><span data-stu-id="524af-253">f.</span></span> <span data-ttu-id="524af-254">Seleccione **Administrator** (Administrador).</span><span class="sxs-lookup"><span data-stu-id="524af-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="524af-255">g.</span><span class="sxs-lookup"><span data-stu-id="524af-255">g.</span></span> <span data-ttu-id="524af-256">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="524af-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="524af-257">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="524af-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="524af-258">En esta sección, concederá acceso a Britta Simon a Moxtra para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="524af-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="524af-260">**Para asignar Britta Simon a Moxtra, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="524af-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="524af-261">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="524af-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="524af-263">En la lista de aplicaciones, seleccione **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="524af-263">In the applications list, select **Moxtra**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="524af-265">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="524af-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="524af-267">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="524af-267">Click **Add** button.</span></span> <span data-ttu-id="524af-268">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="524af-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="524af-270">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="524af-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="524af-271">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="524af-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="524af-272">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="524af-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="524af-273">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="524af-273">Testing single sign-on</span></span>

<span data-ttu-id="524af-274">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="524af-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="524af-275">Al hacer clic en el icono de Moxtra en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Moxtra.</span><span class="sxs-lookup"><span data-stu-id="524af-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="524af-276">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="524af-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="524af-277">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="524af-277">Additional resources</span></span>

* [<span data-ttu-id="524af-278">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="524af-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="524af-279">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="524af-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

