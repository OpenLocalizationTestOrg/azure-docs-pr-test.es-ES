---
title: "Tutorial: integración de Azure Active Directory con LogicMonitor | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="3d48c-103">Tutorial: Integración de Azure Active Directory con LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="3d48c-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="3d48c-104">En este tutorial, aprenderá a integrar LogicMonitor con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d48c-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d48c-105">La integración de LogicMonitor con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3d48c-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d48c-106">Puede controlar en Azure AD quién tiene acceso a LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="3d48c-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="3d48c-107">Puede permitir que los usuarios inicien sesión automáticamente en LogicMonitor (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d48c-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d48c-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3d48c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3d48c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d48c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d48c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3d48c-110">Prerequisites</span></span>

<span data-ttu-id="3d48c-111">Para configurar la integración de Azure AD con LogicMonitor, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3d48c-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="3d48c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d48c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d48c-113">Una suscripción habilitada para el inicio de sesión único en LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="3d48c-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d48c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3d48c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d48c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3d48c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d48c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3d48c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d48c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d48c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d48c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3d48c-118">Scenario description</span></span>
<span data-ttu-id="3d48c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3d48c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d48c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3d48c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d48c-121">Adición de LogicMonitor desde la galería</span><span class="sxs-lookup"><span data-stu-id="3d48c-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="3d48c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d48c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="3d48c-123">Adición de LogicMonitor desde la galería</span><span class="sxs-lookup"><span data-stu-id="3d48c-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="3d48c-124">Para configurar la integración de LogicMonitor en Azure AD, deberá agregar LogicMonitor desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3d48c-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d48c-125">**Para agregar LogicMonitor desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3d48c-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d48c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d48c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d48c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3d48c-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d48c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3d48c-133">En el cuadro de búsqueda, escriba **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-133">In the search box, type **LogicMonitor**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="3d48c-135">En el panel de resultados, seleccione **LogicMonitor** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d48c-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d48c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d48c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d48c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con LogicMonitor con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d48c-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d48c-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LogicMonitor para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d48c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="3d48c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="3d48c-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="3d48c-141">Para establecer la relación de vínculo, en LogicMonitor, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3d48c-142">Para configurar y probar el inicio de sesión único de Azure AD con LogicMonitor, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3d48c-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d48c-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3d48c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d48c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d48c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d48c-145">**[Creación de un usuario de prueba de LogicMonitor](#creating-a-logicmonitor-test-user)**: el objetivo es tener un homólogo de Britta Simon en LogicMonitor que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d48c-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d48c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d48c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d48c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3d48c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d48c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d48c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d48c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="3d48c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="3d48c-150">**Para configurar el inicio de sesión único de Azure AD con LogicMonitor, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d48c-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="3d48c-151">En la página de integración de la aplicación **LogicMonitor** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3d48c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3d48c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="3d48c-155">En la sección **Dominio y direcciones URL de LogicMonitor**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3d48c-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="3d48c-157">a.</span><span class="sxs-lookup"><span data-stu-id="3d48c-157">a.</span></span> <span data-ttu-id="3d48c-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.logicmonitor.com`.</span><span class="sxs-lookup"><span data-stu-id="3d48c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="3d48c-159">b.</span><span class="sxs-lookup"><span data-stu-id="3d48c-159">b.</span></span> <span data-ttu-id="3d48c-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="3d48c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d48c-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3d48c-161">These values are not real.</span></span> <span data-ttu-id="3d48c-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3d48c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3d48c-163">Póngase en contacto con el [equipo de atención al cliente de LogicMonitor](https://www.logicmonitor.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="3d48c-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="3d48c-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3d48c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="3d48c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3d48c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3d48c-168">Inicie sesión como administrador en el sitio de la compañía de **LogicMonitor** .</span><span class="sxs-lookup"><span data-stu-id="3d48c-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="3d48c-169">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="3d48c-170">![Configuración](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="3d48c-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="3d48c-171">En la barra de navegación del lado izquierdo, haga clic en **Inicio de sesión único**</span><span class="sxs-lookup"><span data-stu-id="3d48c-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="3d48c-172">![Inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="3d48c-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="3d48c-173">En la sección **Configuración del inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3d48c-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="3d48c-174">![Configuración de inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="3d48c-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="3d48c-175">a.</span><span class="sxs-lookup"><span data-stu-id="3d48c-175">a.</span></span> <span data-ttu-id="3d48c-176">Seleccione **Habilitar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="3d48c-177">b.</span><span class="sxs-lookup"><span data-stu-id="3d48c-177">b.</span></span> <span data-ttu-id="3d48c-178">En **Default Role Assignment** (Asignación de rol predeterminado), seleccione **readonly**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="3d48c-179">c.</span><span class="sxs-lookup"><span data-stu-id="3d48c-179">c.</span></span> <span data-ttu-id="3d48c-180">Abra el archivo de metadatos descargado en el Bloc de notas y luego pegue el contenido del archivo en el cuadro de texto **Metadatos del proveedor de identidades** .</span><span class="sxs-lookup"><span data-stu-id="3d48c-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="3d48c-181">d.</span><span class="sxs-lookup"><span data-stu-id="3d48c-181">d.</span></span> <span data-ttu-id="3d48c-182">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3d48c-183">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d48c-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d48c-184">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3d48c-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d48c-185">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d48c-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d48c-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d48c-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d48c-187">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d48c-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3d48c-189">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3d48c-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d48c-190">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d48c-192">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d48c-194">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d48c-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d48c-196">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3d48c-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d48c-198">a.</span><span class="sxs-lookup"><span data-stu-id="3d48c-198">a.</span></span> <span data-ttu-id="3d48c-199">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d48c-200">b.</span><span class="sxs-lookup"><span data-stu-id="3d48c-200">b.</span></span> <span data-ttu-id="3d48c-201">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d48c-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d48c-202">c.</span><span class="sxs-lookup"><span data-stu-id="3d48c-202">c.</span></span> <span data-ttu-id="3d48c-203">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3d48c-204">d.</span><span class="sxs-lookup"><span data-stu-id="3d48c-204">d.</span></span> <span data-ttu-id="3d48c-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="3d48c-206">Creación de un usuario de prueba de LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="3d48c-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="3d48c-207">Para que los usuarios de AAD puedan inician sesión, deben aprovisionarse para la aplicación LogicMonitor con sus nombres de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d48c-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="3d48c-208">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="3d48c-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3d48c-209">Inicie sesión como administrador en el sitio de la compañía de LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="3d48c-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="3d48c-210">En el menú de la parte superior, haga clic en **Settings** (Configuración) y, luego, en **Roles and Users** (Roles y usuarios).</span><span class="sxs-lookup"><span data-stu-id="3d48c-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="3d48c-211">![Roles y usuarios](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles y usuarios")</span><span class="sxs-lookup"><span data-stu-id="3d48c-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="3d48c-212">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-212">Click **Add**.</span></span>

4. <span data-ttu-id="3d48c-213">En la sección **Agregar una cuenta** , realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3d48c-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="3d48c-214">![Agregar una cuenta](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Agregar una cuenta")</span><span class="sxs-lookup"><span data-stu-id="3d48c-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="3d48c-215">a.</span><span class="sxs-lookup"><span data-stu-id="3d48c-215">a.</span></span> <span data-ttu-id="3d48c-216">En los cuadros de texto correspondientes, escriba los valores de **Nombre de usuario**, **Correo electrónico**, **Contraseña** y **Vuelva a escribir contraseña** del usuario de Azure Active Directory que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="3d48c-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="3d48c-217">b.</span><span class="sxs-lookup"><span data-stu-id="3d48c-217">b.</span></span> <span data-ttu-id="3d48c-218">Seleccione **Roles**, **Ver permisos** y **Estado**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="3d48c-219">c.</span><span class="sxs-lookup"><span data-stu-id="3d48c-219">c.</span></span> <span data-ttu-id="3d48c-220">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="3d48c-221">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de LogicMonitor que proporcione LogicMonitor para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d48c-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3d48c-222">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d48c-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3d48c-223">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="3d48c-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3d48c-225">**Para asignar a Britta Simon a LogicMonitor, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d48c-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="3d48c-226">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3d48c-228">En la lista de aplicaciones, seleccione **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="3d48c-230">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3d48c-232">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-232">Click **Add** button.</span></span> <span data-ttu-id="3d48c-233">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3d48c-235">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3d48c-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d48c-236">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d48c-237">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3d48c-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d48c-238">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3d48c-238">Testing single sign-on</span></span>

<span data-ttu-id="3d48c-239">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3d48c-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="3d48c-240">Al hacer clic en el icono de LogicMonitor en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="3d48c-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="3d48c-241">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d48c-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3d48c-242">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3d48c-242">Additional resources</span></span>

* [<span data-ttu-id="3d48c-243">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d48c-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d48c-244">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d48c-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

