---
title: "Tutorial: Integración de Azure Active Directory con Box | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="2060b-103">Tutorial: Integración de Azure Active Directory con Box</span><span class="sxs-lookup"><span data-stu-id="2060b-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="2060b-104">En este tutorial, aprenderá a integrar Box con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2060b-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2060b-105">La integración de Box con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2060b-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2060b-106">Puede controlar en Azure AD quién tiene acceso a Box</span><span class="sxs-lookup"><span data-stu-id="2060b-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="2060b-107">Puede permitir que los usuarios inicien sesión automáticamente en Box (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2060b-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2060b-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2060b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2060b-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2060b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2060b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2060b-110">Prerequisites</span></span>

<span data-ttu-id="2060b-111">Para configurar la integración de Azure AD con Box, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2060b-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="2060b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2060b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2060b-113">Una suscripción a Box habilitada para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="2060b-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2060b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2060b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2060b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2060b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2060b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2060b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2060b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2060b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2060b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2060b-118">Scenario description</span></span>
<span data-ttu-id="2060b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2060b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2060b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2060b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2060b-121">Adición de Box desde la galería</span><span class="sxs-lookup"><span data-stu-id="2060b-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="2060b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2060b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="2060b-123">Adición de Box desde la galería</span><span class="sxs-lookup"><span data-stu-id="2060b-123">Adding Box from the gallery</span></span>
<span data-ttu-id="2060b-124">Para configurar la integración de Box en Azure AD, es preciso agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2060b-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2060b-125">**Para agregar Box desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2060b-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2060b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2060b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2060b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2060b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2060b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2060b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2060b-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2060b-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2060b-133">En el cuadro de búsqueda, escriba **Box**.</span><span class="sxs-lookup"><span data-stu-id="2060b-133">In the search box, type **Box**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="2060b-135">En el panel de resultados, seleccione **Box** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2060b-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2060b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2060b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2060b-138">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con Box con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2060b-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2060b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Box para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2060b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="2060b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Box.</span><span class="sxs-lookup"><span data-stu-id="2060b-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="2060b-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Box.</span><span class="sxs-lookup"><span data-stu-id="2060b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="2060b-142">Para configurar y probar el inicio de sesión único de Azure AD con Box, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2060b-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2060b-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2060b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2060b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2060b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2060b-145">**[Creación de un usuario de prueba de Box](#creating-a-box-test-user)**: para tener un homólogo de Britta Simon en Box vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2060b-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2060b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2060b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2060b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2060b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2060b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2060b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2060b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Box.</span><span class="sxs-lookup"><span data-stu-id="2060b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="2060b-150">**Para configurar el inicio de sesión único de Azure AD con Box, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2060b-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="2060b-151">En Azure Portal, en la página de integración de la aplicación **Box**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2060b-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2060b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2060b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="2060b-155">En la sección **Dominio y direcciones URL de Box**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2060b-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="2060b-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.box.com`.</span><span class="sxs-lookup"><span data-stu-id="2060b-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2060b-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="2060b-158">This value is not real.</span></span> <span data-ttu-id="2060b-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="2060b-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="2060b-160">Póngase en contacto con el [equipo de atención al cliente de Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="2060b-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="2060b-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2060b-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="2060b-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2060b-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2060b-165">Para configurar SSO para su aplicación, póngase en contacto con el [equipo de soporte técnico de Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) y proporcione el archivo XML descargado.</span><span class="sxs-lookup"><span data-stu-id="2060b-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="2060b-166">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2060b-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2060b-167">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2060b-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2060b-168">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2060b-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2060b-169">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2060b-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="2060b-170">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2060b-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2060b-172">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2060b-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2060b-173">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2060b-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2060b-175">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2060b-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2060b-177">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2060b-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2060b-179">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2060b-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2060b-181">a.</span><span class="sxs-lookup"><span data-stu-id="2060b-181">a.</span></span> <span data-ttu-id="2060b-182">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2060b-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2060b-183">b.</span><span class="sxs-lookup"><span data-stu-id="2060b-183">b.</span></span> <span data-ttu-id="2060b-184">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2060b-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2060b-185">c.</span><span class="sxs-lookup"><span data-stu-id="2060b-185">c.</span></span> <span data-ttu-id="2060b-186">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2060b-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2060b-187">d.</span><span class="sxs-lookup"><span data-stu-id="2060b-187">d.</span></span> <span data-ttu-id="2060b-188">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2060b-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="2060b-189">Creación de usuario de prueba de Box</span><span class="sxs-lookup"><span data-stu-id="2060b-189">Creating a Box test user</span></span>

<span data-ttu-id="2060b-190">En esta sección, se crea un usuario llamado a Britta Simon en Box.</span><span class="sxs-lookup"><span data-stu-id="2060b-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="2060b-191">Box admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2060b-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="2060b-192">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="2060b-192">There is no action item for you in this section.</span></span> <span data-ttu-id="2060b-193">Si el usuario no existe en Box, se crea uno nuevo cuando se intenta acceder a Box.</span><span class="sxs-lookup"><span data-stu-id="2060b-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2060b-194">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2060b-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2060b-195">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Box.</span><span class="sxs-lookup"><span data-stu-id="2060b-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2060b-197">**Para asignar el usuario Britta Simon a Box, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2060b-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="2060b-198">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2060b-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2060b-200">En la lista de aplicaciones, seleccione **Box**.</span><span class="sxs-lookup"><span data-stu-id="2060b-200">In the applications list, select **Box**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="2060b-202">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2060b-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2060b-204">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2060b-204">Click **Add** button.</span></span> <span data-ttu-id="2060b-205">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2060b-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2060b-207">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2060b-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2060b-208">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2060b-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2060b-209">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2060b-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2060b-210">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2060b-210">Testing single sign-on</span></span>

<span data-ttu-id="2060b-211">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2060b-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2060b-212">Al hacer clic en el icono de Box en el panel de acceso, debería obtener la página de inicio de sesión e iniciar sesión automáticamente en su aplicación Box.</span><span class="sxs-lookup"><span data-stu-id="2060b-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2060b-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2060b-213">Additional resources</span></span>

* [<span data-ttu-id="2060b-214">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2060b-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2060b-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2060b-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2060b-216">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="2060b-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

