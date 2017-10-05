---
title: "Tutorial: Integración de Azure Active Directory con YouEarnedIt | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="a48a5-103">Tutorial: Integración de Azure Active Directory con YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="a48a5-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="a48a5-104">En este tutorial, obtendrá información sobre cómo integrar YouEarnedIt con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a48a5-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a48a5-105">La integración de YouEarnedIt con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a48a5-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a48a5-106">Puede controlar en Azure AD quién tiene acceso a YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="a48a5-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="a48a5-107">Puede habilitar a los usuarios para que inicien sesión automáticamente en YouEarnedIt (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a48a5-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a48a5-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a48a5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a48a5-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a48a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a48a5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a48a5-110">Prerequisites</span></span>

<span data-ttu-id="a48a5-111">Para configurar la integración de Azure AD con YouEarnedIt, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a48a5-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="a48a5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a48a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a48a5-113">Una suscripción habilitada para el inicio de sesión único en YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="a48a5-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a48a5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a48a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a48a5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a48a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a48a5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a48a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a48a5-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a48a5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a48a5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a48a5-118">Scenario description</span></span>
<span data-ttu-id="a48a5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a48a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a48a5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a48a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a48a5-121">Incorporación de YouEarnedIt desde la galería</span><span class="sxs-lookup"><span data-stu-id="a48a5-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="a48a5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a48a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="a48a5-123">Incorporación de YouEarnedIt desde la galería</span><span class="sxs-lookup"><span data-stu-id="a48a5-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="a48a5-124">Para configurar la integración de YouEarnedIt en Azure AD, es preciso agregar YouEarnedIt desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a48a5-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a48a5-125">**Para agregar YouEarnedIt desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a48a5-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a48a5-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="a48a5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a48a5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="a48a5-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a48a5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="a48a5-133">En el cuadro de búsqueda, escriba **YouEarnedt**, seleccione **YouEarnedt** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a48a5-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![YouEarnedIt en la lista de resultados](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a48a5-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="a48a5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a48a5-136">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con YouEarnedIt con una usuaria de prueba llamada "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a48a5-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a48a5-137">Para que el inicio de sesión único funcione, Azure AD tiene que saber cuál es el usuario homólogo de YouEarnedIt para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a48a5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="a48a5-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="a48a5-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="a48a5-139">Para establecer la relación de vínculo en YouEarnedIt, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a48a5-140">Para configurar y probar el inicio de sesión único de Azure AD con YouEarnedIt, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a48a5-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a48a5-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="a48a5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a48a5-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a48a5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a48a5-143">**[Creación de un usuario de prueba de YouEarnedIt](#create-a-youearnedit-test-user)**: para tener un homólogo de Britta Simon en YouEarnedIt que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a48a5-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a48a5-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a48a5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a48a5-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="a48a5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a48a5-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a48a5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a48a5-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="a48a5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="a48a5-148">**Para configurar el inicio de sesión único de Azure AD con YouEarnedIt, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a48a5-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="a48a5-149">En Azure Portal, en la página de integración de la aplicación **YouEarnedIt**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="a48a5-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a48a5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="a48a5-153">En la sección **YouEarnedIt Engage Domain and URLs** (Dominio y direcciones URL de YouEarnedIt), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a48a5-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="a48a5-155">a.</span><span class="sxs-lookup"><span data-stu-id="a48a5-155">a.</span></span> <span data-ttu-id="a48a5-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="a48a5-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="a48a5-157">Environment</span><span class="sxs-lookup"><span data-stu-id="a48a5-157">Environment</span></span>  | <span data-ttu-id="a48a5-158">Patrón</span><span class="sxs-lookup"><span data-stu-id="a48a5-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="a48a5-159">Producción</span><span class="sxs-lookup"><span data-stu-id="a48a5-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="a48a5-160">Espacio aislado</span><span class="sxs-lookup"><span data-stu-id="a48a5-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="a48a5-161">b.</span><span class="sxs-lookup"><span data-stu-id="a48a5-161">b.</span></span> <span data-ttu-id="a48a5-162">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="a48a5-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="a48a5-163">Environment</span><span class="sxs-lookup"><span data-stu-id="a48a5-163">Environment</span></span>  | <span data-ttu-id="a48a5-164">Patrón</span><span class="sxs-lookup"><span data-stu-id="a48a5-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="a48a5-165">Producción</span><span class="sxs-lookup"><span data-stu-id="a48a5-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="a48a5-166">Espacio aislado</span><span class="sxs-lookup"><span data-stu-id="a48a5-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="a48a5-167">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="a48a5-167">These values are not real.</span></span> <span data-ttu-id="a48a5-168">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a48a5-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a48a5-169">Póngase en contacto con el [equipo de soporte de cliente de YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="a48a5-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="a48a5-170">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a48a5-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="a48a5-172">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a48a5-172">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a48a5-174">En la sección **Configuración de YouEarnedIt**, haga clic en **Configurar YouEarnedIt** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a48a5-175">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="a48a5-177">Para configurar el inicio de sesión único en **YouEarnedIt**, es preciso enviar el **certificado (Base64)** descargado y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="a48a5-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="a48a5-178">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="a48a5-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a48a5-179">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a48a5-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a48a5-180">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a48a5-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a48a5-181">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a48a5-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a48a5-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a48a5-182">Create an Azure AD test user</span></span>

<span data-ttu-id="a48a5-183">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a48a5-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="a48a5-185">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a48a5-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a48a5-186">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a48a5-188">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a48a5-190">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a48a5-192">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a48a5-192">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a48a5-194">a.</span><span class="sxs-lookup"><span data-stu-id="a48a5-194">a.</span></span> <span data-ttu-id="a48a5-195">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a48a5-196">b.</span><span class="sxs-lookup"><span data-stu-id="a48a5-196">b.</span></span> <span data-ttu-id="a48a5-197">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a48a5-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a48a5-198">c.</span><span class="sxs-lookup"><span data-stu-id="a48a5-198">c.</span></span> <span data-ttu-id="a48a5-199">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a48a5-200">d.</span><span class="sxs-lookup"><span data-stu-id="a48a5-200">d.</span></span> <span data-ttu-id="a48a5-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="a48a5-202">Creación de un usuario de prueba de YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="a48a5-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="a48a5-203">En esta sección, creará una usuaria llamada Britta Simon en YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="a48a5-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="a48a5-204">Colabore con el equipo de soporte técnico de YouEarnedIt para agregar los usuarios a la plataforma de YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="a48a5-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="a48a5-205">YouEarnedIt espera que el proveedor de identidades proporcione una dirección de correo electrónico o un nombre de usuario en el atributo NameID.</span><span class="sxs-lookup"><span data-stu-id="a48a5-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="a48a5-206">Si no se encuentra el nombre de usuario o dirección de correo electrónico correspondiente dentro de la base de datos o estos no coinciden exactamente, se producirá un error en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a48a5-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="a48a5-207">Para que esto se realice correctamente es necesario que las cuentas se importen en el sistema YouEarnedIt antes de la integración de inicio de sesión único (normalmente mediante la importación CSV o API).</span><span class="sxs-lookup"><span data-stu-id="a48a5-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a48a5-208">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a48a5-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="a48a5-209">En esta sección, va a habilitar a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="a48a5-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="a48a5-211">**Para asignar Britta Simon a YouEarnedIt, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a48a5-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="a48a5-212">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a48a5-214">En la lista de aplicaciones, seleccione **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![Vínculo a YouEarnedIt en la lista de aplicaciones](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="a48a5-216">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="a48a5-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-218">Click **Add** button.</span></span> <span data-ttu-id="a48a5-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="a48a5-221">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a48a5-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a48a5-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a48a5-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a48a5-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a48a5-224">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a48a5-224">Test single sign-on</span></span>

<span data-ttu-id="a48a5-225">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a48a5-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a48a5-226">Al hacer clic en el icono de YouEarnedIt en el panel de acceso, debería iniciar sesión automáticamente en su aplicación YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="a48a5-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="a48a5-227">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a48a5-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a48a5-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a48a5-228">Additional resources</span></span>

* [<span data-ttu-id="a48a5-229">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a48a5-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a48a5-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a48a5-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

