---
title: "Tutorial: Integración de Azure Active Directory con Neota Logic Studio | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Neota Logic Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 99018277392cab44a6b579ad45b4611739a803d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="3f20c-103">Tutorial: Integración de Azure Active Directory con Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="3f20c-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="3f20c-104">En este tutorial, obtendrá información sobre cómo integrar Neota Logic Studio con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f20c-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f20c-105">La integración de Neota Logic Studio con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3f20c-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f20c-106">Puede controlar en Azure AD quién tiene acceso a Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="3f20c-107">Puede permitir que los usuarios inicien sesión automáticamente en Neota Logic Studio (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f20c-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f20c-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3f20c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3f20c-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="3f20c-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="3f20c-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="3f20c-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f20c-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3f20c-111">Prerequisites</span></span>

<span data-ttu-id="3f20c-112">Para configurar la integración de Azure AD con Neota Logic Studio, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3f20c-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="3f20c-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f20c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="3f20c-114">Una suscripción habilitada para inicio de sesión único en Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="3f20c-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f20c-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3f20c-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f20c-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3f20c-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f20c-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3f20c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f20c-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f20c-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f20c-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3f20c-119">Scenario description</span></span>

<span data-ttu-id="3f20c-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3f20c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f20c-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3f20c-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f20c-122">Agregar Neota Logic Studio desde la galería</span><span class="sxs-lookup"><span data-stu-id="3f20c-122">Adding Neota Logic Studio from the gallery</span></span>
2. <span data-ttu-id="3f20c-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f20c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="3f20c-124">Agregar Neota Logic Studio desde la galería</span><span class="sxs-lookup"><span data-stu-id="3f20c-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="3f20c-125">Para configurar la integración de Neota Logic Studio en Azure AD, deberá agregar Neota Logic Studio desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3f20c-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f20c-126">**Para agregar Neota Logic Studio desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3f20c-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f20c-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f20c-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f20c-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3f20c-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3f20c-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3f20c-134">En el cuadro de búsqueda, escriba **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="3f20c-136">En el panel de resultados, seleccione **Neota Logic Studio** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f20c-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f20c-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f20c-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3f20c-139">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Neota Logic Studio con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3f20c-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3f20c-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Neota Logic Studio para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f20c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="3f20c-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="3f20c-142">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="3f20c-143">Para configurar y probar el inicio de sesión único de Azure AD con Neota Logic Studio, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3f20c-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f20c-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3f20c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f20c-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f20c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f20c-146">**[Creación de un usuario de prueba de Neota Logic Studio](#creating-a-neota-logic-studio-test-user)**: para tener un homólogo de Britta Simon en Neota Logic Studio que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="3f20c-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f20c-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f20c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f20c-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3f20c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f20c-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f20c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f20c-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="3f20c-151">**Para configurar el inicio de sesión único de Azure AD con Neota Logic Studio, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3f20c-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="3f20c-152">En Azure Portal, en la página de integración de la aplicación **Neota Logic Studio**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3f20c-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3f20c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="3f20c-156">En la sección **Dominio y direcciones URL de Neota Logic Studio**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3f20c-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="3f20c-158">a.</span><span class="sxs-lookup"><span data-stu-id="3f20c-158">a.</span></span> <span data-ttu-id="3f20c-159">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<sub domain>.neotalogic.com/a/<sub application>`.</span><span class="sxs-lookup"><span data-stu-id="3f20c-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="3f20c-160">b.</span><span class="sxs-lookup"><span data-stu-id="3f20c-160">b.</span></span> <span data-ttu-id="3f20c-161">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="3f20c-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3f20c-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3f20c-162">These values are not the real.</span></span> <span data-ttu-id="3f20c-163">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3f20c-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="3f20c-164">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="3f20c-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="3f20c-165">Póngase en contacto con el [equipo de soporte de cliente de Neota Logic Studio](https://www.neotalogic.com/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="3f20c-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="3f20c-166">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3f20c-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="3f20c-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3f20c-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3f20c-170">Para configurar SSO para su aplicación, póngase en contacto con el [equipo de soporte técnico de Neota Logic Studio](https://www.neotalogic.com/contact-us/) y proporcione el archivo **XML de metadatos** descargado.</span><span class="sxs-lookup"><span data-stu-id="3f20c-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="3f20c-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f20c-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3f20c-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3f20c-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3f20c-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f20c-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f20c-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f20c-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f20c-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3f20c-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3f20c-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3f20c-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f20c-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f20c-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f20c-182">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3f20c-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f20c-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3f20c-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f20c-186">a.</span><span class="sxs-lookup"><span data-stu-id="3f20c-186">a.</span></span> <span data-ttu-id="3f20c-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f20c-188">b.</span><span class="sxs-lookup"><span data-stu-id="3f20c-188">b.</span></span> <span data-ttu-id="3f20c-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f20c-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f20c-190">c.</span><span class="sxs-lookup"><span data-stu-id="3f20c-190">c.</span></span> <span data-ttu-id="3f20c-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3f20c-192">d.</span><span class="sxs-lookup"><span data-stu-id="3f20c-192">d.</span></span> <span data-ttu-id="3f20c-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="3f20c-194">Crear un usuario de prueba de Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="3f20c-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="3f20c-195">En esta sección, creará un usuario llamado Britta Simon en Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="3f20c-196">Trabaje con el [equipo de soporte de cliente de Neota Logic Studio](https://www.neotalogic.com/contact-us/) para agregar los usuarios a la plataforma de Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="3f20c-197">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3f20c-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3f20c-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f20c-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3f20c-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3f20c-201">**Para asignar a Britta Simon a Neota Logic Studio, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3f20c-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="3f20c-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3f20c-204">En la lista de aplicaciones, seleccione **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="3f20c-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3f20c-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-208">Click **Add** button.</span></span> <span data-ttu-id="3f20c-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3f20c-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3f20c-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f20c-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f20c-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3f20c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f20c-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3f20c-214">Testing single sign-on</span></span>

<span data-ttu-id="3f20c-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3f20c-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3f20c-216">Haga clic en el icono de Neota Logic Studio en el panel de acceso para que se le redirija a la página de inicio de sesión de la organización.</span><span class="sxs-lookup"><span data-stu-id="3f20c-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="3f20c-217">Después de registrarse correctamente, iniciará sesión en la aplicación Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="3f20c-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="3f20c-218">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3f20c-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="3f20c-219">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3f20c-219">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3f20c-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3f20c-220">Additional resources</span></span>

* [<span data-ttu-id="3f20c-221">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f20c-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f20c-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f20c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

