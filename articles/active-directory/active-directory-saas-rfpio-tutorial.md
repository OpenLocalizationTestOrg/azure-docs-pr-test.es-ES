---
title: "Tutorial: Integración de Azure Active Directory con RFPIO | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="0aaba-103">Tutorial: Integración de Azure Active Directory con RFPIO</span><span class="sxs-lookup"><span data-stu-id="0aaba-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="0aaba-104">En este tutorial, aprenderá a integrar RFPIO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0aaba-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0aaba-105">La integración de RFPIO con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0aaba-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0aaba-106">Puede controlar en Azure AD quién tiene acceso a RFPIO.</span><span class="sxs-lookup"><span data-stu-id="0aaba-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="0aaba-107">Puede permitir que los usuarios inicien sesión automáticamente en RFPIO (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aaba-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0aaba-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0aaba-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="0aaba-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0aaba-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0aaba-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0aaba-110">Prerequisites</span></span>

<span data-ttu-id="0aaba-111">Para configurar la integración de Azure AD con RFPIO, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0aaba-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="0aaba-112">Una suscripción de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aaba-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="0aaba-113">Una suscripción habilitada para el inicio de sesión único en RFPIO</span><span class="sxs-lookup"><span data-stu-id="0aaba-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0aaba-114">No se recomienda usar un entorno de producción para probar los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0aaba-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="0aaba-115">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0aaba-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="0aaba-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0aaba-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="0aaba-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0aaba-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0aaba-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0aaba-118">Scenario description</span></span>
<span data-ttu-id="0aaba-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0aaba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0aaba-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0aaba-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0aaba-121">Adición de RFPIO desde la galería</span><span class="sxs-lookup"><span data-stu-id="0aaba-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="0aaba-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0aaba-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="0aaba-123">Adición de RFPIO desde la galería</span><span class="sxs-lookup"><span data-stu-id="0aaba-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="0aaba-124">Para configurar la integración de RFPIO en Azure AD, es preciso agregar dicha solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0aaba-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="0aaba-125">Para agregar RFPIO desde la galería</span><span class="sxs-lookup"><span data-stu-id="0aaba-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="0aaba-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, seleccione el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0aaba-128">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0aaba-130">Para agregar una nueva aplicación, seleccione el botón **Nueva aplicación** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0aaba-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0aaba-132">En el cuadro de búsqueda, escriba **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-132">In the search box, type **RFPIO**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="0aaba-134">En el panel de resultados, seleccione **RFPIO** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0aaba-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0aaba-136">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="0aaba-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0aaba-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con RFPIO con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0aaba-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0aaba-138">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es la relación entre el usuario homólogo de RFPIO y un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aaba-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="0aaba-139">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de RFPIO.</span><span class="sxs-lookup"><span data-stu-id="0aaba-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="0aaba-140">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de RFPIO.</span><span class="sxs-lookup"><span data-stu-id="0aaba-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0aaba-141">Para configurar y probar el inicio de sesión único de Azure AD con RFPIO, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0aaba-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0aaba-142">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)**: el objetivo es permitir que los usuarios usen esta característica.</span><span class="sxs-lookup"><span data-stu-id="0aaba-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0aaba-143">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**: el objetivo es probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0aaba-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0aaba-144">**[Creación de un usuario de prueba de RFPIO](#creating-a-rfpio-test-user)**: el objetivo es tener un homólogo de Britta Simon en RFPIO que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aaba-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0aaba-145">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)**: el objetivo es permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aaba-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0aaba-146">**[Prueba del inicio de sesión único](#testing-single-sign-on)**: el objetivo es comprobar que la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="0aaba-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0aaba-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0aaba-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0aaba-148">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación RFPIO.</span><span class="sxs-lookup"><span data-stu-id="0aaba-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="0aaba-149">**Para configurar el inicio de sesión único de Azure AD con RFPIO, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0aaba-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="0aaba-150">En la página de integración de la aplicación **RFPIO** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0aaba-152">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0aaba-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="0aaba-154">Vaya a la sección **Dominio y direcciones URL de RFPIO**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="0aaba-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="0aaba-156">a.</span><span class="sxs-lookup"><span data-stu-id="0aaba-156">a.</span></span> <span data-ttu-id="0aaba-157">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="0aaba-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="0aaba-159">b.</span><span class="sxs-lookup"><span data-stu-id="0aaba-159">b.</span></span> <span data-ttu-id="0aaba-160">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="0aaba-161">c.</span><span class="sxs-lookup"><span data-stu-id="0aaba-161">c.</span></span> <span data-ttu-id="0aaba-162">En el cuadro de texto **Estado de la retransmisión**, escriba un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="0aaba-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="0aaba-163">Póngase en contacto con el [equipo de soporte técnico de RFPIO](https://www.rfpio.com/contact/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="0aaba-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="0aaba-164">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="0aaba-165">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="0aaba-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="0aaba-167">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL similar a la siguiente: `https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="0aaba-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="0aaba-168">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0aaba-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="0aaba-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0aaba-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0aaba-172">En otra ventana del explorador web, inicie sesión en el sitio web de **RFPIO** como administrador.</span><span class="sxs-lookup"><span data-stu-id="0aaba-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="0aaba-173">Haga clic en la lista desplegable de la esquina inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="0aaba-173">Click on the bottom left corner dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="0aaba-175">Haga clic en **Organization Settings** (Configuración de la organización).</span><span class="sxs-lookup"><span data-stu-id="0aaba-175">Click on the **Organization Settings**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="0aaba-177">Haga clic en **FEATURES & INTEGRATION** (CARACTERÍSTICAS E INTEGRACIÓN).</span><span class="sxs-lookup"><span data-stu-id="0aaba-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="0aaba-179">En **SAML SSO Configuration** (Configuración del inicio de sesión único de SAML), haga clic en **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="0aaba-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="0aaba-181">En esta sección, realice las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="0aaba-181">In this Section perform following actions:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="0aaba-183">a.</span><span class="sxs-lookup"><span data-stu-id="0aaba-183">a.</span></span> <span data-ttu-id="0aaba-184">Copie el contenido del archivo **XML de metadatos descargado** y péguelo en el campo **identity configuration** (Configuración de identidad).</span><span class="sxs-lookup"><span data-stu-id="0aaba-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="0aaba-185">Para copiar el contenido del archivo **XML de metadatos** descargado, use **Notepad++** o un **Editor XML** adecuado.</span><span class="sxs-lookup"><span data-stu-id="0aaba-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="0aaba-186">b.</span><span class="sxs-lookup"><span data-stu-id="0aaba-186">b.</span></span> <span data-ttu-id="0aaba-187">Haga clic en **Validar**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-187">Click **Validate**.</span></span>

    <span data-ttu-id="0aaba-188">c.</span><span class="sxs-lookup"><span data-stu-id="0aaba-188">c.</span></span> <span data-ttu-id="0aaba-189">Después de hacer clic en **Validate** (Validar), mueva **SAML(Enabled)** (SAML [Habilitado]) a activado.</span><span class="sxs-lookup"><span data-stu-id="0aaba-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="0aaba-190">d.</span><span class="sxs-lookup"><span data-stu-id="0aaba-190">d.</span></span> <span data-ttu-id="0aaba-191">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="0aaba-192">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0aaba-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0aaba-193">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0aaba-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0aaba-194">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0aaba-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0aaba-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0aaba-195">Create an Azure AD test user</span></span>
<span data-ttu-id="0aaba-196">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0aaba-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0aaba-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0aaba-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0aaba-199">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0aaba-201">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0aaba-203">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0aaba-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0aaba-205">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0aaba-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0aaba-207">a.</span><span class="sxs-lookup"><span data-stu-id="0aaba-207">a.</span></span> <span data-ttu-id="0aaba-208">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0aaba-209">b.</span><span class="sxs-lookup"><span data-stu-id="0aaba-209">b.</span></span> <span data-ttu-id="0aaba-210">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0aaba-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0aaba-211">c.</span><span class="sxs-lookup"><span data-stu-id="0aaba-211">c.</span></span> <span data-ttu-id="0aaba-212">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0aaba-213">d.</span><span class="sxs-lookup"><span data-stu-id="0aaba-213">d.</span></span> <span data-ttu-id="0aaba-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="0aaba-215">Creación de un usuario de prueba de RFPIO</span><span class="sxs-lookup"><span data-stu-id="0aaba-215">Create a RFPIO test user</span></span>

<span data-ttu-id="0aaba-216">Para permitir que los usuarios de Azure AD inicien sesión en RFPIO, deben aprovisionarse en dicha solución.</span><span class="sxs-lookup"><span data-stu-id="0aaba-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="0aaba-217">En el caso de RFPIO, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="0aaba-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="0aaba-218">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0aaba-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0aaba-219">Regístrese en el sitio de la compañía de RFPIO como administrador.</span><span class="sxs-lookup"><span data-stu-id="0aaba-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="0aaba-220">Haga clic en la lista desplegable de la esquina inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="0aaba-220">Click on the bottom left corner dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="0aaba-222">Haga clic en **Organization Settings** (Configuración de la organización).</span><span class="sxs-lookup"><span data-stu-id="0aaba-222">Click on the **Organization Settings**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="0aaba-224">Haga clic en **TEAM MEMBERS** (MIEMBROS DE EQUIPO).</span><span class="sxs-lookup"><span data-stu-id="0aaba-224">Click **TEAM MEMBERS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="0aaba-226">Haga clic en **ADD MEMBERS** (AGREGAR MIEMBROS).</span><span class="sxs-lookup"><span data-stu-id="0aaba-226">Click on **ADD MEMBERS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="0aaba-228">Vaya a la sección **Add New Members** (Agregar nuevos miembros).</span><span class="sxs-lookup"><span data-stu-id="0aaba-228">In the **Add New Members** section.</span></span> <span data-ttu-id="0aaba-229">Realice las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="0aaba-229">Perform following actions:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="0aaba-231">a.</span><span class="sxs-lookup"><span data-stu-id="0aaba-231">a.</span></span> <span data-ttu-id="0aaba-232">Escriba la **dirección de correo electrónico** en el campo **Enter one email per line** (Escribir un correo electrónico por línea).</span><span class="sxs-lookup"><span data-stu-id="0aaba-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="0aaba-233">b.</span><span class="sxs-lookup"><span data-stu-id="0aaba-233">b.</span></span> <span data-ttu-id="0aaba-234">Seleccione **Role** (Role) de acuerdo con sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="0aaba-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="0aaba-235">c.</span><span class="sxs-lookup"><span data-stu-id="0aaba-235">c.</span></span> <span data-ttu-id="0aaba-236">Haga clic en **ADD MEMBERS** (AGREGAR MIEMBROS).</span><span class="sxs-lookup"><span data-stu-id="0aaba-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="0aaba-237">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="0aaba-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0aaba-238">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0aaba-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="0aaba-239">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a RFPIO.</span><span class="sxs-lookup"><span data-stu-id="0aaba-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0aaba-241">**Para asignar a Britta Simon a RFPIO, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0aaba-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="0aaba-242">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0aaba-244">En la lista de aplicaciones, seleccione **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-244">In the applications list, select **RFPIO**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="0aaba-246">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0aaba-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-248">Click **Add** button.</span></span> <span data-ttu-id="0aaba-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0aaba-251">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0aaba-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0aaba-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0aaba-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0aaba-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0aaba-254">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0aaba-254">Test single sign-on</span></span>

<span data-ttu-id="0aaba-255">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0aaba-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="0aaba-256">Al hacer clic en el icono de RFPIO en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación RFPIO.</span><span class="sxs-lookup"><span data-stu-id="0aaba-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="0aaba-257">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0aaba-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0aaba-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0aaba-258">Additional resources</span></span>

* [<span data-ttu-id="0aaba-259">Lista de tutoriales sobre cómo la integración de aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0aaba-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0aaba-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0aaba-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

