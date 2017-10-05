---
title: "Tutorial: integración de Azure Active Directory con Directions on Microsoft | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Directions on Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="9550a-103">Tutorial: Integración de Azure Active Directory con Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="9550a-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="9550a-104">En este tutorial, aprenderá a integrar Directions on Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9550a-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9550a-105">La integración de Directions on Microsoft con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9550a-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9550a-106">Puede controlar en Azure AD quién tiene acceso a Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9550a-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="9550a-107">Puede permitir que los usuarios inicien sesión automáticamente en Directions on Microsoft (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9550a-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9550a-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9550a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9550a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9550a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9550a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9550a-110">Prerequisites</span></span>

<span data-ttu-id="9550a-111">Para configurar la integración de Azure AD con Directions on Microsoft, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9550a-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="9550a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9550a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9550a-113">Una suscripción habilitada para el inicio de sesión único en Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="9550a-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9550a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9550a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9550a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9550a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9550a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9550a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9550a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9550a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9550a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9550a-118">Scenario description</span></span>
<span data-ttu-id="9550a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9550a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9550a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9550a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9550a-121">Adición de Directions on Microsoft desde la galería</span><span class="sxs-lookup"><span data-stu-id="9550a-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="9550a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9550a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="9550a-123">Adición de Directions on Microsoft desde la galería</span><span class="sxs-lookup"><span data-stu-id="9550a-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="9550a-124">Para configurar la integración de Directions on Microsoft en Azure AD, deberá agregar Directions on Microsoft desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9550a-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9550a-125">**Para agregar Directions on Microsoft desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9550a-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9550a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9550a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9550a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9550a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9550a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9550a-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9550a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9550a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9550a-133">En el cuadro de búsqueda, escriba **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="9550a-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="9550a-135">En el panel de resultados, seleccione **Directions on Microsoft**y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9550a-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9550a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9550a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9550a-138">En esta sección, va a configurar y probar el inicio de sesión único de Microsoft Azure AD con Directions on Microsoft con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9550a-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9550a-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Directions on Microsoft para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9550a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="9550a-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9550a-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="9550a-141">Para establecer la relación de vínculo, en Directions on Microsoft, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9550a-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9550a-142">Para configurar y probar el inicio de sesión único de Microsoft Azure AD con Directions on Microsoft, es preciso completar los siguientes pasos preliminares:</span><span class="sxs-lookup"><span data-stu-id="9550a-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9550a-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9550a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9550a-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9550a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9550a-145">**[Creación de un usuario de prueba de Directions on Microsoft](#creating-a-directions-on-microsoft-test-user)**: para tener un homólogo de Britta Simon en Directions on Microsoft que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9550a-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9550a-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9550a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9550a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9550a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9550a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9550a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9550a-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9550a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="9550a-150">**Para configurar el inicio de sesión único de Azure AD con Directions on Microsoft, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9550a-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="9550a-151">En Azure Portal, en la página de integración de la aplicación **Directions on Microsoft**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9550a-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9550a-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9550a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="9550a-155">En la sección **Dominio y direcciones URL de Directions on Microsoft**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9550a-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="9550a-157">a.</span><span class="sxs-lookup"><span data-stu-id="9550a-157">a.</span></span> <span data-ttu-id="9550a-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="9550a-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="9550a-159">b.</span><span class="sxs-lookup"><span data-stu-id="9550a-159">b.</span></span> <span data-ttu-id="9550a-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="9550a-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="9550a-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9550a-161">These values are not real.</span></span> <span data-ttu-id="9550a-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9550a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9550a-163">Póngase en contacto con el [equipo de soporte técnico de Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9550a-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="9550a-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9550a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="9550a-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9550a-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9550a-168">Para configurar el inicio de sesión único en **Directions on Microsoft**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="9550a-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="9550a-169">Para que el equipo de soporte técnico de Directions on Microsoft pueda buscar su pertenencia al sitio federado, incluya la información de su compañía en el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="9550a-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="9550a-170">El inicio de sesión único de Directions on Microsoft debe habilitarlo el [equipo de soporte técnico de cliente de Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="9550a-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="9550a-171">Recibirá una notificación cuando se haya habilitado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9550a-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="9550a-172">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9550a-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9550a-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9550a-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9550a-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9550a-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9550a-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9550a-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="9550a-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9550a-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9550a-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9550a-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9550a-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9550a-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9550a-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9550a-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9550a-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9550a-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9550a-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9550a-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9550a-187">a.</span><span class="sxs-lookup"><span data-stu-id="9550a-187">a.</span></span> <span data-ttu-id="9550a-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9550a-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9550a-189">b.</span><span class="sxs-lookup"><span data-stu-id="9550a-189">b.</span></span> <span data-ttu-id="9550a-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9550a-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9550a-191">c.</span><span class="sxs-lookup"><span data-stu-id="9550a-191">c.</span></span> <span data-ttu-id="9550a-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9550a-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9550a-193">d.</span><span class="sxs-lookup"><span data-stu-id="9550a-193">d.</span></span> <span data-ttu-id="9550a-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9550a-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="9550a-195">Creación de un usuario de prueba de Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="9550a-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="9550a-196">No hay ningún elemento de acción para que configure el aprovisionamiento de usuarios para Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9550a-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="9550a-197">Cuando un usuario asignado intenta iniciar sesión en Directions on Microsoft desde el Panel de acceso, Directions on Microsoft comprueba si el usuario existe.</span><span class="sxs-lookup"><span data-stu-id="9550a-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="9550a-198">Si no hay cuentas de usuario disponibles, Directions on Microsoft crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9550a-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9550a-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9550a-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9550a-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9550a-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9550a-202">**Para asignar a Britta Simon a Directions on Microsoft, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9550a-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="9550a-203">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9550a-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9550a-205">En la lista de aplicaciones, seleccione **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="9550a-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="9550a-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9550a-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9550a-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9550a-209">Click **Add** button.</span></span> <span data-ttu-id="9550a-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9550a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9550a-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9550a-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9550a-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9550a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9550a-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9550a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9550a-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9550a-215">Testing single sign-on</span></span>

<span data-ttu-id="9550a-216">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9550a-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="9550a-217">Al hacer clic en el icono de Directions on Microsoft en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9550a-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="9550a-218">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9550a-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9550a-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9550a-219">Additional resources</span></span>

* [<span data-ttu-id="9550a-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9550a-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9550a-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9550a-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

