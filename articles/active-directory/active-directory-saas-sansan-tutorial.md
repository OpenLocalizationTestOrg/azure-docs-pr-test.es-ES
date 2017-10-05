---
title: "Tutorial: Integración de Azure Active Directory con Sansan | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Sansan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e1a9653d5feea910308cefabdbdfe3a6af44bbe4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="9fe47-103">Tutorial: Integración de Azure Active Directory con Sansan</span><span class="sxs-lookup"><span data-stu-id="9fe47-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="9fe47-104">En este tutorial, obtendrá información sobre cómo integrar Sansan con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fe47-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9fe47-105">Integrar Sansan con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9fe47-105">Integrating Sansan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9fe47-106">Puede controlar en Azure AD quién tiene acceso a Sansan.</span><span class="sxs-lookup"><span data-stu-id="9fe47-106">You can control in Azure AD who has access to Sansan</span></span>
- <span data-ttu-id="9fe47-107">Puede permitir que los usuarios inicien sesión automáticamente en Sansan (Inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fe47-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9fe47-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9fe47-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9fe47-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9fe47-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fe47-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9fe47-110">Prerequisites</span></span>

<span data-ttu-id="9fe47-111">Para configurar la integración de Azure AD con Sansan, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9fe47-111">To configure Azure AD integration with Sansan, you need the following items:</span></span>

- <span data-ttu-id="9fe47-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9fe47-113">Una suscripción habilitada para el inicio de sesión único en Sansan</span><span class="sxs-lookup"><span data-stu-id="9fe47-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9fe47-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9fe47-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9fe47-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9fe47-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9fe47-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9fe47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9fe47-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9fe47-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9fe47-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9fe47-118">Scenario description</span></span>
<span data-ttu-id="9fe47-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9fe47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9fe47-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9fe47-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fe47-121">Incorporación de Sansan desde la galería</span><span class="sxs-lookup"><span data-stu-id="9fe47-121">Adding Sansan from the gallery</span></span>
2. <span data-ttu-id="9fe47-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-the-gallery"></a><span data-ttu-id="9fe47-123">Incorporación de Sansan desde la galería</span><span class="sxs-lookup"><span data-stu-id="9fe47-123">Adding Sansan from the gallery</span></span>
<span data-ttu-id="9fe47-124">Para configurar la integración de Sansan en Azure AD, deberá agregar Sansan desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9fe47-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9fe47-125">**Para agregar Sansan desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9fe47-125">**To add Sansan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe47-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9fe47-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9fe47-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9fe47-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9fe47-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9fe47-133">En el cuadro de búsqueda, escriba **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-133">In the search box, type **Sansan**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="9fe47-135">En el panel de resultados, seleccione **Sansan** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe47-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9fe47-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9fe47-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sansan con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9fe47-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9fe47-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Sansan para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fe47-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span></span> <span data-ttu-id="9fe47-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Sansan.</span><span class="sxs-lookup"><span data-stu-id="9fe47-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span></span>

<span data-ttu-id="9fe47-141">Para establecer la relación de vínculo, en Sansan, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9fe47-142">Para configurar y probar el inicio de sesión único de Azure AD con Sansan, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9fe47-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9fe47-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9fe47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9fe47-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9fe47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fe47-145">**[Creación de un usuario de prueba de Sansan](#creating-a-sansan-test-user)**: para tener un homólogo de Britta Simon en Sansan que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fe47-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9fe47-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fe47-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fe47-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9fe47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9fe47-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9fe47-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Sansan.</span><span class="sxs-lookup"><span data-stu-id="9fe47-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="9fe47-150">**Para configurar el inicio de sesión único de Azure AD con Sansan, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9fe47-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe47-151">En Azure Portal, en la página de integración de la aplicación **Sansan**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9fe47-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9fe47-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="9fe47-155">En la sección **Dominio y direcciones URL de Sansan**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9fe47-155">On the **Sansan Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="9fe47-157">a.</span><span class="sxs-lookup"><span data-stu-id="9fe47-157">a.</span></span> <span data-ttu-id="9fe47-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="9fe47-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | <span data-ttu-id="9fe47-159">Environment</span><span class="sxs-lookup"><span data-stu-id="9fe47-159">Environment</span></span> | <span data-ttu-id="9fe47-160">URL</span><span class="sxs-lookup"><span data-stu-id="9fe47-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="9fe47-161">Web de PC</span><span class="sxs-lookup"><span data-stu-id="9fe47-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="9fe47-162">Aplicación nativa móvil</span><span class="sxs-lookup"><span data-stu-id="9fe47-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="9fe47-163">Configuración del explorador móvil</span><span class="sxs-lookup"><span data-stu-id="9fe47-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="9fe47-164">b.</span><span class="sxs-lookup"><span data-stu-id="9fe47-164">b.</span></span> <span data-ttu-id="9fe47-165">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="9fe47-165">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="9fe47-166">Environment</span><span class="sxs-lookup"><span data-stu-id="9fe47-166">Environment</span></span>             | <span data-ttu-id="9fe47-167">URL</span><span class="sxs-lookup"><span data-stu-id="9fe47-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="9fe47-168">Web de PC</span><span class="sxs-lookup"><span data-stu-id="9fe47-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="9fe47-169">Aplicación nativa móvil</span><span class="sxs-lookup"><span data-stu-id="9fe47-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="9fe47-170">Configuración del explorador móvil</span><span class="sxs-lookup"><span data-stu-id="9fe47-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="9fe47-171">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9fe47-171">These values are not real.</span></span> <span data-ttu-id="9fe47-172">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9fe47-172">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9fe47-173">Póngase en contacto con el [equipo de soporte al cliente de Sansan](https://www.sansan.com/form/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9fe47-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span></span> 

4. <span data-ttu-id="9fe47-174">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9fe47-174">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="9fe47-176">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9fe47-176">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9fe47-178">En la sección **Configuración de Sansan**, haga clic en **Configurar Sansan** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-178">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9fe47-179">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="9fe47-181">Para configurar el inicio de sesión único en **Sansan**, es preciso enviar el **certificado** descargado, la **dirección URL de cierre de sesión**, el **identificador de identidad de SAML** y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="9fe47-181">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="9fe47-182">El equipo de soporte técnico lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="9fe47-182">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="9fe47-183">La configuración del explorador de PC también funciona para aplicaciones y exploradores móviles junto con la web del PC.</span><span class="sxs-lookup"><span data-stu-id="9fe47-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="9fe47-184">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe47-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9fe47-185">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9fe47-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9fe47-186">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9fe47-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9fe47-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe47-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9fe47-188">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9fe47-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9fe47-190">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9fe47-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe47-191">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9fe47-193">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9fe47-195">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9fe47-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fe47-197">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9fe47-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9fe47-199">a.</span><span class="sxs-lookup"><span data-stu-id="9fe47-199">a.</span></span> <span data-ttu-id="9fe47-200">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9fe47-201">b.</span><span class="sxs-lookup"><span data-stu-id="9fe47-201">b.</span></span> <span data-ttu-id="9fe47-202">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9fe47-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9fe47-203">c.</span><span class="sxs-lookup"><span data-stu-id="9fe47-203">c.</span></span> <span data-ttu-id="9fe47-204">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9fe47-205">d.</span><span class="sxs-lookup"><span data-stu-id="9fe47-205">d.</span></span> <span data-ttu-id="9fe47-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="9fe47-207">Creación de un usuario de prueba de Sansan</span><span class="sxs-lookup"><span data-stu-id="9fe47-207">Creating a Sansan test user</span></span>

<span data-ttu-id="9fe47-208">En esta sección, creará un usuario llamado Britta Simon en SanSan.</span><span class="sxs-lookup"><span data-stu-id="9fe47-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="9fe47-209">La aplicación Sansan necesita que todos los usuarios estén aprovisionados en la aplicación antes de realizar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9fe47-209">SanSan application needs the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="9fe47-210">Si necesita crear un usuario de forma manual o por lotes de usuarios, póngase en contacto con el [equipo de soporte técnico de Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="9fe47-210">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9fe47-211">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe47-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9fe47-212">En esta sección, concederá acceso a Britta Simon a Sansan para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe47-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9fe47-214">**Para asignar Britta Simon a Sansan, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9fe47-214">**To assign Britta Simon to Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe47-215">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9fe47-217">En la lista de aplicaciones, seleccione **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-217">In the applications list, select **Sansan**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="9fe47-219">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9fe47-221">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-221">Click **Add** button.</span></span> <span data-ttu-id="9fe47-222">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9fe47-224">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9fe47-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9fe47-225">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9fe47-226">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9fe47-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9fe47-227">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9fe47-227">Testing single sign-on</span></span>

<span data-ttu-id="9fe47-228">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9fe47-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9fe47-229">Al hacer clic en el icono de Sansan en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Sansan.</span><span class="sxs-lookup"><span data-stu-id="9fe47-229">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span></span>
<span data-ttu-id="9fe47-230">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9fe47-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fe47-231">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9fe47-231">Additional resources</span></span>

* [<span data-ttu-id="9fe47-232">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fe47-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fe47-233">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9fe47-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

