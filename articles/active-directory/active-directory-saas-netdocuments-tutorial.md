---
title: "Tutorial: Integración de Azure Active Directory con NetDocuments | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="9229f-103">Tutorial: Integración de Azure Active Directory con NetDocuments</span><span class="sxs-lookup"><span data-stu-id="9229f-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="9229f-104">En este tutorial, aprenderá a integrar NetDocuments con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9229f-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9229f-105">La integración de NetDocuments con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9229f-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9229f-106">Puede controlar en Azure AD quién tiene acceso a NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="9229f-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="9229f-107">Puede permitir que los usuarios inicien sesión automáticamente en NetDocuments (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9229f-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9229f-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9229f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9229f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9229f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9229f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9229f-110">Prerequisites</span></span>

<span data-ttu-id="9229f-111">Para configurar la integración de Azure AD con NetDocuments, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9229f-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="9229f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9229f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9229f-113">Una suscripción habilitada para el inicio de sesión único en NetDocuments</span><span class="sxs-lookup"><span data-stu-id="9229f-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9229f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9229f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9229f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9229f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9229f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9229f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9229f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9229f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9229f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9229f-118">Scenario description</span></span>
<span data-ttu-id="9229f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9229f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9229f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9229f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9229f-121">Adición de NetDocuments desde la galería</span><span class="sxs-lookup"><span data-stu-id="9229f-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="9229f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9229f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="9229f-123">Adición de NetDocuments desde la galería</span><span class="sxs-lookup"><span data-stu-id="9229f-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="9229f-124">Para configurar la integración de NetDocuments en Azure AD, es preciso agregar dicha solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9229f-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9229f-125">**Para agregar NetDocuments desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9229f-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9229f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9229f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9229f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9229f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9229f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9229f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9229f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9229f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9229f-133">En el cuadro de búsqueda, escriba **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="9229f-133">In the search box, type **NetDocuments**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="9229f-135">En el panel de resultados, seleccione **NetDocuments** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9229f-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9229f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9229f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9229f-138">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con NetDocuments con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9229f-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9229f-139">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de NetDocuments para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9229f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="9229f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="9229f-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="9229f-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="9229f-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9229f-142">Para configurar y probar el inicio de sesión único de Azure AD con NetDocuments, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9229f-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9229f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9229f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9229f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9229f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9229f-145">**[Creación de un usuario de prueba de NetDocuments](#creating-a-netdocuments-test-user)**: el objetivo es tener un homólogo de Britta Simon en NetDocuments que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9229f-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9229f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9229f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9229f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9229f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9229f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9229f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9229f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="9229f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="9229f-150">**Para configurar el inicio de sesión único de Azure AD con NetDocuments, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9229f-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="9229f-151">En la página de integración de la aplicación **NetDocuments** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9229f-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9229f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9229f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="9229f-155">En la sección **Dominio y direcciones URL de NetDocuments**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9229f-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="9229f-157">a.</span><span class="sxs-lookup"><span data-stu-id="9229f-157">a.</span></span> <span data-ttu-id="9229f-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`.</span><span class="sxs-lookup"><span data-stu-id="9229f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="9229f-159">b.</span><span class="sxs-lookup"><span data-stu-id="9229f-159">b.</span></span> <span data-ttu-id="9229f-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`.</span><span class="sxs-lookup"><span data-stu-id="9229f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9229f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9229f-161">These values are not real.</span></span> <span data-ttu-id="9229f-162">Actualice estos valores con los valores reales de URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9229f-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="9229f-163">Póngase en contacto con [equipo de soporte técnico de NetDocuments](https://support.netdocuments.com/hc/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9229f-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="9229f-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9229f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="9229f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9229f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9229f-168">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de la compañía de NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="9229f-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="9229f-169">Vaya a **Administración**.</span><span class="sxs-lookup"><span data-stu-id="9229f-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="9229f-170">Haga clic en **Agregar y quitar usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9229f-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="9229f-171">![Repositorio](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositorio")</span><span class="sxs-lookup"><span data-stu-id="9229f-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="9229f-172">Haga clic en **Configurar opciones de autenticación avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="9229f-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="9229f-173">![Configurar opciones de autenticación avanzadas](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurar opciones de autenticación avanzadas")</span><span class="sxs-lookup"><span data-stu-id="9229f-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="9229f-174">En el cuadro de diálogo **Federated Identity** (Identidad federada), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9229f-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="9229f-175">![Identidad federada](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identidad federada")</span><span class="sxs-lookup"><span data-stu-id="9229f-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="9229f-176">a.</span><span class="sxs-lookup"><span data-stu-id="9229f-176">a.</span></span> <span data-ttu-id="9229f-177">Como **Tipo de servidor de identidad federada**, seleccione **Servicios de federación de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9229f-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="9229f-178">b.</span><span class="sxs-lookup"><span data-stu-id="9229f-178">b.</span></span> <span data-ttu-id="9229f-179">Haga clic en el botón **Choose file** (Elegir archivo) para cargar el archivo de metadatos que descargó de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9229f-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="9229f-180">c.</span><span class="sxs-lookup"><span data-stu-id="9229f-180">c.</span></span> <span data-ttu-id="9229f-181">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9229f-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="9229f-182">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9229f-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9229f-183">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9229f-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9229f-184">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9229f-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9229f-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9229f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="9229f-186">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9229f-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9229f-188">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9229f-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9229f-189">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9229f-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9229f-191">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9229f-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9229f-193">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9229f-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9229f-195">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9229f-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9229f-197">a.</span><span class="sxs-lookup"><span data-stu-id="9229f-197">a.</span></span> <span data-ttu-id="9229f-198">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9229f-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9229f-199">b.</span><span class="sxs-lookup"><span data-stu-id="9229f-199">b.</span></span> <span data-ttu-id="9229f-200">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9229f-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9229f-201">c.</span><span class="sxs-lookup"><span data-stu-id="9229f-201">c.</span></span> <span data-ttu-id="9229f-202">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9229f-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9229f-203">d.</span><span class="sxs-lookup"><span data-stu-id="9229f-203">d.</span></span> <span data-ttu-id="9229f-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9229f-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="9229f-205">Creación de un usuario de prueba de NetDocuments</span><span class="sxs-lookup"><span data-stu-id="9229f-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="9229f-206">Para permitir que los usuarios de Azure AD inicien sesión en NetDocuments, deben aprovisionarse en dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="9229f-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="9229f-207">En el caso de NetDocuments, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9229f-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="9229f-208">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="9229f-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9229f-209">Inicie sesión como administrador en el sitio de la compañía **NetDocuments** .</span><span class="sxs-lookup"><span data-stu-id="9229f-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="9229f-210">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="9229f-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="9229f-211">![Administración](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="9229f-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="9229f-212">Haga clic en **Agregar y quitar usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9229f-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="9229f-213">![Repositorio](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositorio")</span><span class="sxs-lookup"><span data-stu-id="9229f-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="9229f-214">En el cuadro de texto **Dirección de correo electrónico**, escriba la dirección de correo electrónico de la cuenta válida de Azure Active Directory que quiera aprovisionar y haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="9229f-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="9229f-215">![Dirección de correo electrónico](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Dirección de correo electrónico")</span><span class="sxs-lookup"><span data-stu-id="9229f-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="9229f-216">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="9229f-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="9229f-217">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de NetDocuments ofrecida por NetDocuments para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9229f-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9229f-218">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9229f-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9229f-219">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="9229f-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9229f-221">**Para asignar Britta Simon a NetDocuments, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9229f-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="9229f-222">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9229f-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9229f-224">En la lista de aplicaciones, seleccione **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="9229f-224">In the applications list, select **NetDocuments**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="9229f-226">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9229f-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9229f-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9229f-228">Click **Add** button.</span></span> <span data-ttu-id="9229f-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9229f-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9229f-231">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9229f-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9229f-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9229f-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9229f-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9229f-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9229f-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9229f-234">Testing single sign-on</span></span>

<span data-ttu-id="9229f-235">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9229f-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9229f-236">Al hacer clic en el icono de NetDocuments en el Panel de acceso, debería iniciar sesión automáticamente en dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="9229f-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="9229f-237">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9229f-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9229f-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9229f-238">Additional resources</span></span>

* [<span data-ttu-id="9229f-239">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9229f-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9229f-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9229f-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

