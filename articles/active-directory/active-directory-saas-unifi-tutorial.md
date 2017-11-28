---
title: "Tutorial: Integración de Azure Active Directory con UNIFI | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 09074d4628825909f0bb961c8001e53fb06cf7c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="82923-103">Tutorial: Integración de Azure Active Directory con UNIFI</span><span class="sxs-lookup"><span data-stu-id="82923-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="82923-104">En este tutorial, aprenderá a integrar UNIFI con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82923-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82923-105">La integración de UNIFI con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="82923-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82923-106">Puede controlar en Azure AD quién tiene acceso a UNIFI.</span><span class="sxs-lookup"><span data-stu-id="82923-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="82923-107">Puede permitir que los usuarios inicien sesión automáticamente en UNIFI (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82923-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82923-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="82923-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="82923-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82923-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82923-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="82923-110">Prerequisites</span></span>

<span data-ttu-id="82923-111">Para configurar la integración de Azure AD con UNIFI, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="82923-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="82923-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82923-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82923-113">Una suscripción habilitada para el inicio de sesión único en UNIFI</span><span class="sxs-lookup"><span data-stu-id="82923-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82923-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="82923-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82923-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="82923-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82923-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="82923-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82923-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82923-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82923-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="82923-118">Scenario description</span></span>
<span data-ttu-id="82923-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="82923-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82923-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="82923-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82923-121">Adición de UNIFI desde la galería</span><span class="sxs-lookup"><span data-stu-id="82923-121">Adding UNIFI from the gallery</span></span>
2. <span data-ttu-id="82923-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82923-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="82923-123">Adición de UNIFI desde la galería</span><span class="sxs-lookup"><span data-stu-id="82923-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="82923-124">Para configurar la integración de UNIFI en Azure AD, es preciso agregar dicha solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="82923-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82923-125">**Para agregar UNIFI desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="82923-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82923-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82923-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82923-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="82923-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82923-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="82923-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="82923-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82923-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="82923-133">En el cuadro de texto, escriba **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="82923-133">In the search box, type **UNIFI**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="82923-135">En el panel de resultados, seleccione **UNIFI** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82923-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82923-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82923-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82923-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con UNIFI con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="82923-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="82923-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de UNIFI para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82923-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="82923-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de UNIFI.</span><span class="sxs-lookup"><span data-stu-id="82923-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="82923-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de UNIFI.</span><span class="sxs-lookup"><span data-stu-id="82923-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82923-142">Para configurar y probar el inicio de sesión único de Azure AD con UNIFI, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="82923-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82923-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="82923-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="82923-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82923-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82923-145">**[Creación de un usuario de prueba de UNIFI](#creating-a-unifi-test-user)**: el objetivo es tener un homólogo de Britta Simon en UNIFI que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82923-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="82923-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82923-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82923-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="82923-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82923-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82923-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82923-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación UNIFI.</span><span class="sxs-lookup"><span data-stu-id="82923-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="82923-150">**Para configurar el inicio de sesión único de Azure AD con UNIFI, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="82923-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="82923-151">En la página de integración de la aplicación **UNIFI** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="82923-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="82923-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="82923-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="82923-155">Vaya a la sección **Dominio y direcciones URL de UNIFI**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="82923-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="82923-157">En el cuadro de texto **Identificador**, escriba el valor `INVIEWlabs`.</span><span class="sxs-lookup"><span data-stu-id="82923-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="82923-158">Active **Mostrar configuración avanzada de URL**, si quiere configurar la aplicación en modo iniciado por **SP**.</span><span class="sxs-lookup"><span data-stu-id="82923-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="82923-160">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="82923-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="82923-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="82923-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="82923-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="82923-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="82923-165">En la sección **Configuración de UNIFI**, haga clic en **Configurar UNIFI** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="82923-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="82923-166">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="82923-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="82923-168">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de **UNIFI** como administrador.</span><span class="sxs-lookup"><span data-stu-id="82923-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="82923-169">Haga clic en la pestaña **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="82923-169">Click on the **Users**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="82923-171">Haga clic en **Add New Identity Provider** (Agregar nuevo proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="82923-171">Click on the **Add New Identity Provider**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="82923-173">En la sección **Add Identity Provider** (Agregar proveedor de identidades), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="82923-173">In the **Add Identity Provider** section, perform the following steps:</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="82923-175">a.</span><span class="sxs-lookup"><span data-stu-id="82923-175">a.</span></span> <span data-ttu-id="82923-176">En el cuadro de texto **Provider Name** (Nombre del proveedor, escriba el nombre del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="82923-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="82923-177">b.</span><span class="sxs-lookup"><span data-stu-id="82923-177">b.</span></span> <span data-ttu-id="82923-178">En el cuadro de texto **SAML Login URL** (Dirección URL de inicio de sesión de SAML), pegue el valor de **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="82923-178">In the the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="82923-179">c.</span><span class="sxs-lookup"><span data-stu-id="82923-179">c.</span></span> <span data-ttu-id="82923-180">Abra el certificado que ha descargado de Azure Portal en el Bloc de notas, quite las etiquetas **---BEGIN CERTIFICATE---** y **---END CERTIFICATE---** y pegue el resto del contenido en el cuadro de texto **Certificate** (Certificado).</span><span class="sxs-lookup"><span data-stu-id="82923-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="82923-181">d.</span><span class="sxs-lookup"><span data-stu-id="82923-181">d.</span></span> <span data-ttu-id="82923-182">Active la casilla **is Default Provider** (Es el proveedor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="82923-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="82923-183">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82923-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82923-184">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="82923-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82923-185">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82923-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82923-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82923-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="82923-187">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="82923-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="82923-189">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="82923-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82923-190">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82923-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82923-192">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="82923-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82923-194">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82923-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82923-196">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="82923-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82923-198">a.</span><span class="sxs-lookup"><span data-stu-id="82923-198">a.</span></span> <span data-ttu-id="82923-199">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82923-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82923-200">b.</span><span class="sxs-lookup"><span data-stu-id="82923-200">b.</span></span> <span data-ttu-id="82923-201">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82923-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82923-202">c.</span><span class="sxs-lookup"><span data-stu-id="82923-202">c.</span></span> <span data-ttu-id="82923-203">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="82923-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="82923-204">d.</span><span class="sxs-lookup"><span data-stu-id="82923-204">d.</span></span> <span data-ttu-id="82923-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="82923-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="82923-206">Creación de un usuario de prueba de UNIFI</span><span class="sxs-lookup"><span data-stu-id="82923-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="82923-207">En esta sección, creará un usuario llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82923-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="82923-208">**UNIFI** admite el aprovisionamiento automático de usuarios, por lo que se requiere ningún paso manual.</span><span class="sxs-lookup"><span data-stu-id="82923-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="82923-209">Los usuarios se crean automáticamente después de autenticarse correctamente en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82923-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="82923-210">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82923-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="82923-211">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a UNIFI.</span><span class="sxs-lookup"><span data-stu-id="82923-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="82923-213">**Para asignar a Britta Simon a UNIFI, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="82923-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="82923-214">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="82923-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="82923-216">En la lista de aplicaciones, seleccione **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="82923-216">In the applications list, select **UNIFI**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="82923-218">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="82923-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="82923-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="82923-220">Click **Add** button.</span></span> <span data-ttu-id="82923-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="82923-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="82923-223">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="82923-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="82923-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="82923-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82923-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="82923-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82923-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="82923-226">Testing single sign-on</span></span>

<span data-ttu-id="82923-227">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="82923-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="82923-228">Al hacer clic en el icono de UNIFI en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación UNIFI.</span><span class="sxs-lookup"><span data-stu-id="82923-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="82923-229">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82923-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="82923-230">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="82923-230">Additional resources</span></span>

* [<span data-ttu-id="82923-231">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82923-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82923-232">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82923-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

