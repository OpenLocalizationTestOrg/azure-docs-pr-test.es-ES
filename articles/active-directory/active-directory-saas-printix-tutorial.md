---
title: "Tutorial: Integración de Azure Active Directory con Printix | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="e9c9b-103">Tutorial: Integración de Azure Active Directory con Printix</span><span class="sxs-lookup"><span data-stu-id="e9c9b-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="e9c9b-104">En este tutorial, obtendrá información sobre cómo integrar Printix con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9c9b-105">La integración de Printix con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e9c9b-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9c9b-106">Puede controlar en Azure AD quién tiene acceso a Printix.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="e9c9b-107">Puede permitir que los usuarios inicien sesión automáticamente en Printix (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9c9b-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e9c9b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9c9b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e9c9b-110">Prerequisites</span></span>

<span data-ttu-id="e9c9b-111">Para configurar la integración de Azure AD con Printix, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e9c9b-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="e9c9b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9c9b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9c9b-113">Una suscripción habilitada para el inicio de sesión único en Printix</span><span class="sxs-lookup"><span data-stu-id="e9c9b-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9c9b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9c9b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e9c9b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9c9b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9c9b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9c9b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e9c9b-118">Scenario description</span></span>
<span data-ttu-id="e9c9b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9c9b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e9c9b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9c9b-121">Adición de Printix desde la galería</span><span class="sxs-lookup"><span data-stu-id="e9c9b-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="e9c9b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9c9b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="e9c9b-123">Adición de Printix desde la galería</span><span class="sxs-lookup"><span data-stu-id="e9c9b-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="e9c9b-124">Para configurar la integración de Printix en Azure AD, deberá agregar Printix desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9c9b-125">**Para agregar Printix desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e9c9b-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9c9b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9c9b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9c9b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e9c9b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e9c9b-133">En el cuadro de búsqueda, escriba **Printix**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-133">In the search box, type **Printix**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="e9c9b-135">En el panel de resultados, seleccione **Printix** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9c9b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9c9b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9c9b-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Printix con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9c9b-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9c9b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Printix para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="e9c9b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Printix.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="e9c9b-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Printix.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e9c9b-142">Para configurar y probar el inicio de sesión único de Azure AD con Printix, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e9c9b-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9c9b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9c9b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9c9b-145">**[Creación de un usuario de prueba en Printix](#creating-a-printix-test-user)**: el objetivo es tener un homólogo de Britta Simon en Printix que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9c9b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9c9b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9c9b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9c9b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9c9b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Printix.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="e9c9b-150">**Para configurar el inicio de sesión único de Azure AD con Printix, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e9c9b-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="e9c9b-151">En la página de integración de la aplicación **Printix** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e9c9b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="e9c9b-155">En la sección **Dominio y direcciones URL de Printix**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e9c9b-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="e9c9b-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.printix.net`.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9c9b-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-158">The value is not real.</span></span> <span data-ttu-id="e9c9b-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="e9c9b-160">Póngase en contacto con el [equipo de atención al cliente de Printix](mailto:support@printix.net) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="e9c9b-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="e9c9b-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e9c9b-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9c9b-165">Inicie la sesión en el inquilino de Printix como administrador.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="e9c9b-166">En el menú de la parte superior, haga clic en el icono situado en la esquina superior derecha y seleccione "**Authentication**" (Autenticación).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="e9c9b-168">En la pestaña **Setup** (Configuración), seleccione **Enable Azure/Office 365 authentication** (Habilitar la autenticación de Azure y Office 365).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="e9c9b-170">En la pestaña **Azure**, escriba la dirección URL de metadatos de federación en el cuadro de texto de "**Federation metadata document**" (Documento de metadatos de federación).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="e9c9b-171">Adjunte el archivo XML de metadatos que descargó de Azure AD al [equipo de soporte técnico de Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="e9c9b-172">Ellos se encargarán de cargar este archivo y le proporcionarán una dirección URL de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="e9c9b-174">Haga clic en el botón "**Test**" (Probar) y, si la prueba se ha realizado correctamente, en el botón "**OK**" (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="e9c9b-175">Después de hacer clic en el botón **Test** (Probar) se mostrará la página de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="e9c9b-176">El mensaje "The test was successful" (La prueba se ha realizado correctamente) aquí significa que después de escribir las credenciales de su cuenta de prueba de Azure se mostrará el mensaje "Settings tested OK" (Configuración probada correctamente). Después, haga clic en el botón **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="e9c9b-178">Haga clic en el botón **Save** (Guardar) en la página "**Authentication**" (Autenticación).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="e9c9b-179">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e9c9b-180">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e9c9b-181">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9c9b-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9c9b-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9c9b-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9c9b-183">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9c9b-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e9c9b-185">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e9c9b-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9c9b-186">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9c9b-188">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9c9b-190">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9c9b-192">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e9c9b-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9c9b-194">a.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-194">a.</span></span> <span data-ttu-id="e9c9b-195">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9c9b-196">b.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-196">b.</span></span> <span data-ttu-id="e9c9b-197">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9c9b-198">c.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-198">c.</span></span> <span data-ttu-id="e9c9b-199">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e9c9b-200">d.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-200">d.</span></span> <span data-ttu-id="e9c9b-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="e9c9b-202">Creación de un usuario de prueba de Printix</span><span class="sxs-lookup"><span data-stu-id="e9c9b-202">Creating a Printix test user</span></span>

<span data-ttu-id="e9c9b-203">El objetivo de esta sección es crear un usuario llamado Britta Simon en Printix.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="e9c9b-204">Printix admite el aprovisionamiento just-in-time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e9c9b-205">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-205">There is no action item for you in this section.</span></span> <span data-ttu-id="e9c9b-206">Al intentar acceder a Printix, se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="e9c9b-207">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el [equipo de soporte técnico de Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="e9c9b-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e9c9b-208">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9c9b-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e9c9b-209">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Printix.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e9c9b-211">**Para asignar a Britta Simon a Printix, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e9c9b-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="e9c9b-212">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e9c9b-214">En la lista de aplicaciones, seleccione **Printix**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-214">In the applications list, select **Printix**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="e9c9b-216">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e9c9b-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-218">Click **Add** button.</span></span> <span data-ttu-id="e9c9b-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e9c9b-221">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9c9b-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9c9b-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9c9b-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e9c9b-224">Testing single sign-on</span></span>

<span data-ttu-id="e9c9b-225">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9c9b-226">Al hacer clic en el icono de Printix en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Printix.</span><span class="sxs-lookup"><span data-stu-id="e9c9b-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9c9b-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e9c9b-227">Additional resources</span></span>

* [<span data-ttu-id="e9c9b-228">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9c9b-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9c9b-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9c9b-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

