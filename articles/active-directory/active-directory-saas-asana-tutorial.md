---
title: "Tutorial: Integración de Azure Active Directory con Asana | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: a2f0cecb93cc382bcfd710c44eb70f80ae67f9b6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="bbd73-103">Tutorial: Integración de Azure Active Directory con Asana</span><span class="sxs-lookup"><span data-stu-id="bbd73-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="bbd73-104">En este tutorial, obtendrá información sobre cómo integrar Asana con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbd73-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbd73-105">Integrar Asana con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bbd73-105">Integrating Asana with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbd73-106">Puede controlar en Azure AD quién tiene acceso a Asana.</span><span class="sxs-lookup"><span data-stu-id="bbd73-106">You can control in Azure AD who has access to Asana</span></span>
- <span data-ttu-id="bbd73-107">Puede permitir que los usuarios inicien sesión automáticamente en Asana (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd73-107">You can enable your users to automatically get signed-on to Asana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbd73-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bbd73-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bbd73-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbd73-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbd73-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bbd73-110">Prerequisites</span></span>

<span data-ttu-id="bbd73-111">Para configurar la integración de Azure AD con Asana, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bbd73-111">To configure Azure AD integration with Asana, you need the following items:</span></span>

- <span data-ttu-id="bbd73-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbd73-113">Una suscripción habilitada para el inicio de sesión único en Asana</span><span class="sxs-lookup"><span data-stu-id="bbd73-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbd73-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bbd73-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbd73-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bbd73-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbd73-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bbd73-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbd73-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbd73-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbd73-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bbd73-118">Scenario description</span></span>
<span data-ttu-id="bbd73-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bbd73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbd73-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="bbd73-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbd73-121">Adición de Asana desde la galería</span><span class="sxs-lookup"><span data-stu-id="bbd73-121">Adding Asana from the gallery</span></span>
2. <span data-ttu-id="bbd73-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd73-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-the-gallery"></a><span data-ttu-id="bbd73-123">Adición de Asana desde la galería</span><span class="sxs-lookup"><span data-stu-id="bbd73-123">Adding Asana from the gallery</span></span>
<span data-ttu-id="bbd73-124">Para configurar la integración de Asana en Azure AD, es preciso agregar Asana desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="bbd73-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbd73-125">**Para agregar Asana desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bbd73-125">**To add Asana from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd73-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="bbd73-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbd73-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="bbd73-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bbd73-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="bbd73-133">En el cuadro de búsqueda, escriba **Asana**, seleccione **Asana** en el panel de resultados y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbd73-133">In the search box, type **Asana**, select **Asana** from result panel then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bbd73-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd73-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bbd73-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Asana con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bbd73-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bbd73-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Asana para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd73-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span></span> <span data-ttu-id="bbd73-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Asana.</span><span class="sxs-lookup"><span data-stu-id="bbd73-138">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span></span>

<span data-ttu-id="bbd73-139">Para establecer la relación de vínculo, en Asana, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-139">In Asana, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bbd73-140">Para configurar y probar el inicio de sesión único de Azure AD con Asana, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bbd73-140">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbd73-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="bbd73-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bbd73-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd73-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbd73-143">**[Creación de un usuario de prueba de Asana](#create-an-asana-test-user)**: para tener un homólogo de Britta Simon en Asana que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd73-143">**[Create an Asana test user](#create-an-asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbd73-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd73-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbd73-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="bbd73-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bbd73-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd73-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bbd73-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Asana.</span><span class="sxs-lookup"><span data-stu-id="bbd73-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="bbd73-148">**Para configurar el inicio de sesión único de Azure AD con Asana, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bbd73-148">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd73-149">En Azure Portal, en la página de integración de la aplicación **Asana**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-149">In the Azure portal, on the **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bbd73-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bbd73-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="bbd73-153">En la sección **Dominio y direcciones URL de Asana**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bbd73-153">On the **Asana Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="bbd73-155">a.</span><span class="sxs-lookup"><span data-stu-id="bbd73-155">a.</span></span> <span data-ttu-id="bbd73-156">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://app.asana.com/`.</span><span class="sxs-lookup"><span data-stu-id="bbd73-156">In the **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="bbd73-157">b.</span><span class="sxs-lookup"><span data-stu-id="bbd73-157">b.</span></span> <span data-ttu-id="bbd73-158">En el cuadro de texto **Identificador**, escriba el valor: `https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="bbd73-158">In the **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="bbd73-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bbd73-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="bbd73-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bbd73-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bbd73-163">En la sección **Configuración de Asana**, haga clic en **Configurar Asana** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-163">On the **Asana Configuration** section, click **Configure Asana** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bbd73-164">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="bbd73-166">En una ventana de explorador diferente, inicie sesión en su aplicación de Asana como administrador.</span><span class="sxs-lookup"><span data-stu-id="bbd73-166">In a different browser window, sign-on to your Asana application.</span></span> <span data-ttu-id="bbd73-167">Para configurar SSO en Asana, acceda a la configuración del área de trabajo haciendo clic en el nombre del área de trabajo en la esquina superior derecha de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="bbd73-167">To configure SSO in Asana, access the workspace settings by clicking the workspace name on the top right corner of the screen.</span></span> <span data-ttu-id="bbd73-168">Después, haga clic en la **configuración del \<nombre del área de trabajo\>**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Configuración de SSO de Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="bbd73-170">En la ventana **Organization settings** (Configuración de la organización), haga clic en **Administration** (Administración).</span><span class="sxs-lookup"><span data-stu-id="bbd73-170">On the **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="bbd73-171">Después, haga clic en **Members must log in via SAML** (Los miembros deben iniciar sesión mediante SAML) para habilitar la configuración de SSO.</span><span class="sxs-lookup"><span data-stu-id="bbd73-171">Then, click **Members must log in via SAML** to enable the SSO configuration.</span></span> <span data-ttu-id="bbd73-172">Lleve a cabo los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="bbd73-172">The perform the following steps:</span></span>
   
    ![Definición de la configuración de la organización de inicio de sesión único](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="bbd73-174">a.</span><span class="sxs-lookup"><span data-stu-id="bbd73-174">a.</span></span> <span data-ttu-id="bbd73-175">En el cuadro de texto **Sign-in page URL** (Dirección URL de la página de inicio de sesión), pegue la **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="bbd73-175">In the **Sign-in page URL** textbox, paste the **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="bbd73-176">b.</span><span class="sxs-lookup"><span data-stu-id="bbd73-176">b.</span></span> <span data-ttu-id="bbd73-177">Haga clic con el botón derecho en el certificado descargado de Azure Portal y después abra el archivo de certificado con el Bloc de notas o el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="bbd73-177">Right click the certificate downloaded from Azure portal, then open the certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="bbd73-178">Copie el contenido entre el título inicial y final del certificado y péguelo en el cuadro de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-178">Copy the content between the begin and the end certificate title and paste it in the **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="bbd73-179">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-179">Click **Save**.</span></span> <span data-ttu-id="bbd73-180">Vaya a la [guía de Asana para configurar el SSO](https://asana.com/guide/help/premium/authentication#gl-saml) si necesita más ayuda.</span><span class="sxs-lookup"><span data-stu-id="bbd73-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="bbd73-181">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbd73-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bbd73-182">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="bbd73-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bbd73-183">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbd73-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bbd73-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd73-184">Create an Azure AD test user</span></span>

<span data-ttu-id="bbd73-185">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bbd73-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="bbd73-187">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="bbd73-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd73-188">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbd73-190">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbd73-192">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bbd73-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbd73-194">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bbd73-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbd73-196">a.</span><span class="sxs-lookup"><span data-stu-id="bbd73-196">a.</span></span> <span data-ttu-id="bbd73-197">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbd73-198">b.</span><span class="sxs-lookup"><span data-stu-id="bbd73-198">b.</span></span> <span data-ttu-id="bbd73-199">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd73-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbd73-200">c.</span><span class="sxs-lookup"><span data-stu-id="bbd73-200">c.</span></span> <span data-ttu-id="bbd73-201">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bbd73-202">d.</span><span class="sxs-lookup"><span data-stu-id="bbd73-202">d.</span></span> <span data-ttu-id="bbd73-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="bbd73-204">Creación de un usuario de prueba de Asana</span><span class="sxs-lookup"><span data-stu-id="bbd73-204">Create an Asana test user</span></span>

<span data-ttu-id="bbd73-205">En esta sección, creará un usuario llamado Britta Simon en Asana.</span><span class="sxs-lookup"><span data-stu-id="bbd73-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="bbd73-206">En **Asana**, vaya a la sección **Teams** (Equipos) en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="bbd73-206">On **Asana**, go to the **Teams** section on the left panel.</span></span> <span data-ttu-id="bbd73-207">Haga clic en el botón de signo más.</span><span class="sxs-lookup"><span data-stu-id="bbd73-207">Click the plus sign button.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="bbd73-209">Escriba el correo electrónico britta.simon@contoso.com en el cuadro de texto y, después, seleccione **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-209">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span></span>

3. <span data-ttu-id="bbd73-210">Haga clic en **Enviar invitación**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-210">Click **Send Invite**.</span></span> <span data-ttu-id="bbd73-211">El nuevo usuario recibirá un correo electrónico en su cuenta de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="bbd73-211">The new user will receive an email into her email account.</span></span> <span data-ttu-id="bbd73-212">Tendrá que crear y validar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="bbd73-212">She will need to create and validate the account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bbd73-213">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd73-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="bbd73-214">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Asana.</span><span class="sxs-lookup"><span data-stu-id="bbd73-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asana.</span></span>

![Asignación del rol de usuario][200]

<span data-ttu-id="bbd73-216">**Para asignar Britta Simon a Asana, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bbd73-216">**To assign Britta Simon to Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd73-217">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bbd73-219">En la lista de aplicaciones, seleccione **Asana**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-219">In the applications list, select **Asana**.</span></span>

    ![Vínculo a Asana en la lista de aplicaciones](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="bbd73-221">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="bbd73-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-223">Click **Add** button.</span></span> <span data-ttu-id="bbd73-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="bbd73-226">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="bbd73-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bbd73-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbd73-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bbd73-229">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="bbd73-229">Test single sign-on</span></span>

<span data-ttu-id="bbd73-230">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd73-230">The objective of this section is to test your Azure AD single sign-on.</span></span>

<span data-ttu-id="bbd73-231">Vaya a la página de inicio de sesión de Asana.</span><span class="sxs-lookup"><span data-stu-id="bbd73-231">Go to Asana login page.</span></span> <span data-ttu-id="bbd73-232">En el cuadro de texto Email address (Dirección de correo electrónico), escriba la dirección de correo electrónico britta.simon@contoso.com. Deje el cuadro de texto de contraseña en blanco y, después, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="bbd73-232">In the Email address textbox, insert the email address britta.simon@contoso.com. Leave the password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="bbd73-233">Se le redirigirá a la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd73-233">You will be redirected to Azure AD login page.</span></span> <span data-ttu-id="bbd73-234">Complete sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd73-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="bbd73-235">Ya ha iniciado sesión en Asana.</span><span class="sxs-lookup"><span data-stu-id="bbd73-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bbd73-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bbd73-236">Additional resources</span></span>

* [<span data-ttu-id="bbd73-237">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbd73-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbd73-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbd73-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
