---
title: "Tutorial: Integración de Azure Active Directory con BeeLine | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="289aa-103">Tutorial: Integración de Azure Active Directory con BeeLine</span><span class="sxs-lookup"><span data-stu-id="289aa-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="289aa-104">En este tutorial, obtendrá información sobre cómo integrar BeeLine con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="289aa-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="289aa-105">Integrar BeeLine con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="289aa-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="289aa-106">Puede controlar en Azure AD quién tiene acceso a BeeLine</span><span class="sxs-lookup"><span data-stu-id="289aa-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="289aa-107">Puede permitir que los usuarios inicien sesión automáticamente en BeeLine (Inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="289aa-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="289aa-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="289aa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="289aa-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="289aa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="289aa-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="289aa-110">Prerequisites</span></span>

<span data-ttu-id="289aa-111">Para configurar la integración de Azure AD con BeeLine, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="289aa-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="289aa-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="289aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="289aa-113">Una suscripción habilitada para inicio de sesión único en BeeLine</span><span class="sxs-lookup"><span data-stu-id="289aa-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="289aa-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="289aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="289aa-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="289aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="289aa-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="289aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="289aa-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="289aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="289aa-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="289aa-118">Scenario description</span></span>
<span data-ttu-id="289aa-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="289aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="289aa-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="289aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="289aa-121">Agregar BeeLine desde la galería</span><span class="sxs-lookup"><span data-stu-id="289aa-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="289aa-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="289aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="289aa-123">Agregar BeeLine desde la galería</span><span class="sxs-lookup"><span data-stu-id="289aa-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="289aa-124">Para configurar la integración de BeeLine en Azure AD, deberá agregar BeeLine desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="289aa-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="289aa-125">**Para agregar BeeLine desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="289aa-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="289aa-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="289aa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="289aa-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="289aa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="289aa-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="289aa-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="289aa-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="289aa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="289aa-133">En el cuadro de búsqueda, escriba **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="289aa-133">In the search box, type **BeeLine**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="289aa-135">En el panel de resultados, seleccione **BeeLine** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="289aa-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="289aa-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="289aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="289aa-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BeeLine con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="289aa-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="289aa-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BeeLine para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="289aa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="289aa-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BeeLine.</span><span class="sxs-lookup"><span data-stu-id="289aa-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="289aa-141">Para establecer la relación de vínculo, en BeeLine, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="289aa-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="289aa-142">Para configurar y probar el inicio de sesión único de Azure AD con BeeLine, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="289aa-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="289aa-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="289aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="289aa-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="289aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="289aa-145">**[Creación de un usuario de prueba de BeeLine](#creating-a-beeline-test-user)**: para tener un homólogo de Britta Simon en BeeLine que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="289aa-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="289aa-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="289aa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="289aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="289aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="289aa-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="289aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="289aa-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación BeeLine.</span><span class="sxs-lookup"><span data-stu-id="289aa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="289aa-150">**Para configurar el inicio de sesión único de Azure AD con BeeLine, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="289aa-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="289aa-151">En Azure Portal, en la página de integración de la aplicación **BeeLine**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="289aa-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="289aa-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="289aa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="289aa-155">En la sección **Dominio y direcciones URL de BeeLine**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="289aa-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="289aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="289aa-157">a.</span></span> <span data-ttu-id="289aa-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="289aa-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="289aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="289aa-159">b.</span></span> <span data-ttu-id="289aa-160">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="289aa-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="289aa-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="289aa-161">These values are not real.</span></span> <span data-ttu-id="289aa-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="289aa-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="289aa-163">Póngase en contacto con el [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="289aa-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="289aa-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="289aa-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="289aa-166">La aplicación Beeline espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="289aa-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="289aa-167">Trabaje primero con el [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) para identificar el identificador de usuario correcto que se asignará a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="289aa-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="289aa-168">También siga las instrucciones del [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) sobre el atributo que desean usar para esta asignación.</span><span class="sxs-lookup"><span data-stu-id="289aa-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="289aa-169">Puede administrar el valor de este atributo desde la pestaña **User Attributes** (Atributos de usuario) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="289aa-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="289aa-170">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="289aa-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="289aa-171">Aquí hemos asignado la notificación **User Identifier** (Identificador de usuario) con el atributo **userprincipalname**, que proporciona el identificador de usuario único, que se enviará a la aplicación BeeLine en cada respuesta de SAML correcta.</span><span class="sxs-lookup"><span data-stu-id="289aa-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="289aa-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="289aa-173">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="289aa-175">En la sección **Configuración de BeeLine**, haga clic en **Configurar BeeLine** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="289aa-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="289aa-176">Copie los valores de **Sign-Out URL** (Dirección URL de cierre de sesión) y **SAML Entity IDe** (Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="289aa-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="289aa-178">Para configurar el inicio de sesión único en **BeeLine**, debe enviar los datos descargados de **XML de metadatos**, **SAML Entity ID** (Identificador de entidad de SAML) y **Sign-Out URL** (dirección URL de cierre de sesión) al [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="289aa-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="289aa-179">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="289aa-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="289aa-180">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="289aa-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="289aa-181">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="289aa-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="289aa-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="289aa-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="289aa-183">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="289aa-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="289aa-185">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="289aa-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="289aa-186">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="289aa-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="289aa-188">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="289aa-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="289aa-190">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="289aa-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="289aa-192">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="289aa-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="289aa-194">a.</span><span class="sxs-lookup"><span data-stu-id="289aa-194">a.</span></span> <span data-ttu-id="289aa-195">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="289aa-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="289aa-196">b.</span><span class="sxs-lookup"><span data-stu-id="289aa-196">b.</span></span> <span data-ttu-id="289aa-197">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="289aa-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="289aa-198">c.</span><span class="sxs-lookup"><span data-stu-id="289aa-198">c.</span></span> <span data-ttu-id="289aa-199">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="289aa-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="289aa-200">d.</span><span class="sxs-lookup"><span data-stu-id="289aa-200">d.</span></span> <span data-ttu-id="289aa-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="289aa-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="289aa-202">Creación de un usuario de prueba de BeeLine</span><span class="sxs-lookup"><span data-stu-id="289aa-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="289aa-203">En esta sección, creará un usuario llamado Britta Simon en Beeline.</span><span class="sxs-lookup"><span data-stu-id="289aa-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="289aa-204">La aplicación BeeLine necesita que todos los usuarios estén aprovisionados en la aplicación antes de realizar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="289aa-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="289aa-205">Trabaje con el [servicio de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) para aprovisionar todos estos usuarios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="289aa-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="289aa-206">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="289aa-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="289aa-207">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BeeLine.</span><span class="sxs-lookup"><span data-stu-id="289aa-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="289aa-209">**Para asignar a Britta Simon a BeeLine, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="289aa-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="289aa-210">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="289aa-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="289aa-212">En la lista de aplicaciones, seleccione **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="289aa-212">In the applications list, select **BeeLine**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="289aa-214">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="289aa-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="289aa-216">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="289aa-216">Click **Add** button.</span></span> <span data-ttu-id="289aa-217">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="289aa-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="289aa-219">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="289aa-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="289aa-220">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="289aa-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="289aa-221">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="289aa-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="289aa-222">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="289aa-222">Testing single sign-on</span></span>

<span data-ttu-id="289aa-223">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="289aa-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="289aa-224">Al hacer clic en el icono de Beeline en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Beeline.</span><span class="sxs-lookup"><span data-stu-id="289aa-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="289aa-225">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="289aa-225">Additional resources</span></span>

* [<span data-ttu-id="289aa-226">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="289aa-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="289aa-227">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="289aa-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

