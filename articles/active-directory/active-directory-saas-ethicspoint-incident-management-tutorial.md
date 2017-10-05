---
title: "Tutorial: Integración de Azure Active Directory con EthicsPoint Incident Management (EPIM) | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y EthicsPoint Incident Management (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: b5ac3afd973b5765ba151e766754934b49ac0e0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="1fbc1-103">Tutorial: Integración de Azure Active Directory con EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="1fbc1-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="1fbc1-104">En este tutorial, aprenderá a integrar EthicsPoint Incident Management (EPIM) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-104">In this tutorial, you learn how to integrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fbc1-105">La integración de EthicsPoint Incident Management (EPIM) con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1fbc1-106">Puede controlar en Azure AD quién tiene acceso a EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-106">You can control in Azure AD who has access to EthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="1fbc1-107">Puede permitir que los usuarios inicien sesión automáticamente en EthicsPoint Incident Management (EPIM) (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-107">You can enable your users to automatically get signed-on to EthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1fbc1-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1fbc1-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fbc1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1fbc1-110">Prerequisites</span></span>

<span data-ttu-id="1fbc1-111">Para configurar la integración de Azure AD con EthicsPoint Incident Management (EPIM), necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-111">To configure Azure AD integration with EthicsPoint Incident Management (EPIM), you need the following items:</span></span>

- <span data-ttu-id="1fbc1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fbc1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fbc1-113">Una suscripción habilitada para el inicio de sesión único en EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="1fbc1-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fbc1-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fbc1-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fbc1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fbc1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fbc1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1fbc1-118">Scenario description</span></span>
<span data-ttu-id="1fbc1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fbc1-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fbc1-121">Adición de EthicsPoint Incident Management (EPIM) desde la galería</span><span class="sxs-lookup"><span data-stu-id="1fbc1-121">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
2. <span data-ttu-id="1fbc1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fbc1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-the-gallery"></a><span data-ttu-id="1fbc1-123">Adición de EthicsPoint Incident Management (EPIM) desde la galería</span><span class="sxs-lookup"><span data-stu-id="1fbc1-123">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
<span data-ttu-id="1fbc1-124">Para configurar la integración de EthicsPoint Incident Management (EPIM) en Azure AD, debe agregar EthicsPoint Incident Management (EPIM) desde la galería a su lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-124">To configure the integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need to add EthicsPoint Incident Management (EPIM) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1fbc1-125">**Para agregar EthicsPoint Incident Management (EPIM) desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fbc1-125">**To add EthicsPoint Incident Management (EPIM) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fbc1-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1fbc1-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1fbc1-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1fbc1-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1fbc1-133">En el cuadro de búsqueda, escriba **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-133">In the search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="1fbc1-135">En el panel de resultados, seleccione **EthicsPoint Incident Management (EPIM)** y, a continuación, haga clic en **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-135">In the results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1fbc1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fbc1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1fbc1-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con EthicsPoint Incident Management (EPIM) con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1fbc1-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1fbc1-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de EthicsPoint Incident Management (EPIM) para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EthicsPoint Incident Management (EPIM) is to a user in Azure AD.</span></span> <span data-ttu-id="1fbc1-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-140">In other words, a link relationship between an Azure AD user and the related user in EthicsPoint Incident Management (EPIM) needs to be established.</span></span>

<span data-ttu-id="1fbc1-141">Para establecer la relación de vínculo, en EthicsPoint Incident Management (EPIM), asigne el valor del **nombre de usuario** en Azure AD como valor del **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-141">In EthicsPoint Incident Management (EPIM), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1fbc1-142">Para configurar y probar el inicio de sesión único de Azure AD con EthicsPoint Incident Management (EPIM), es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-142">To configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1fbc1-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1fbc1-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fbc1-145">**[Creación de un usuario de prueba de EthicsPoint Incident Management (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)**: para tener un homólogo de Britta Simon en EthicsPoint Incident Management (EPIM) que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - to have a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1fbc1-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fbc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1fbc1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fbc1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1fbc1-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="1fbc1-150">**Para configurar el inicio de sesión único de Azure AD con EthicsPoint Incident Management (EPIM), realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fbc1-150">**To configure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="1fbc1-151">En Azure Portal, en la página de integración de la aplicación **EthicsPoint Incident Management (EPIM)**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-151">In the Azure portal, on the **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1fbc1-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="1fbc1-155">En la sección **Dominio y direcciones URL de EthicsPoint Incident Management (EPIM)**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-155">On the **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="1fbc1-157">a.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-157">a.</span></span> <span data-ttu-id="1fbc1-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="1fbc1-159">b.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-159">b.</span></span> <span data-ttu-id="1fbc1-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="1fbc1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="1fbc1-161">c.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-161">c.</span></span> <span data-ttu-id="1fbc1-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<servername>.navexglobal.com/adfs/ls/`.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1fbc1-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-163">These values are not real.</span></span> <span data-ttu-id="1fbc1-164">Actualícelos con la dirección URL de respuesta, el identificador y la dirección URL de inicio de sesión reales.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-164">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="1fbc1-165">Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) to get these values.</span></span> 

4. <span data-ttu-id="1fbc1-166">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="1fbc1-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1fbc1-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1fbc1-170">Para configurar el inicio de sesión único en **EthicsPoint Incident Management (EPIM)**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-170">To configure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need to send the downloaded **Metadata XML** to [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="1fbc1-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1fbc1-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1fbc1-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1fbc1-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1fbc1-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fbc1-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="1fbc1-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fbc1-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1fbc1-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1fbc1-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1fbc1-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1fbc1-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1fbc1-182">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1fbc1-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1fbc1-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1fbc1-186">a.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-186">a.</span></span> <span data-ttu-id="1fbc1-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fbc1-188">b.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-188">b.</span></span> <span data-ttu-id="1fbc1-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1fbc1-190">c.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-190">c.</span></span> <span data-ttu-id="1fbc1-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1fbc1-192">d.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-192">d.</span></span> <span data-ttu-id="1fbc1-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="1fbc1-194">Creación de un usuario de prueba de EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="1fbc1-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="1fbc1-195">En esta sección, creará un usuario llamado Britta Simon en EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="1fbc1-196">Trabaje con el [equipo de soporte técnico de EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us) para agregar los usuarios a la plataforma de EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) to add the users in the EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1fbc1-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fbc1-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1fbc1-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EthicsPoint Incident Management (EPIM).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1fbc1-200">**Para asignar a Britta Simon a EthicsPoint Incident Management (EPIM), siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1fbc1-200">**To assign Britta Simon to EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="1fbc1-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1fbc1-203">En la lista de aplicaciones, seleccione **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-203">In the applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="1fbc1-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1fbc1-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-207">Click **Add** button.</span></span> <span data-ttu-id="1fbc1-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1fbc1-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1fbc1-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1fbc1-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1fbc1-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1fbc1-213">Testing single sign-on</span></span>

<span data-ttu-id="1fbc1-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1fbc1-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="1fbc1-215">Al hacer clic en el icono de EthicsPoint Incident Management (EPIM) en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="1fbc1-215">When you click the EthicsPoint Incident Management (EPIM) tile in the Access Panel, you should get automatically signed-on to your EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fbc1-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1fbc1-216">Additional resources</span></span>

* [<span data-ttu-id="1fbc1-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fbc1-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fbc1-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fbc1-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

