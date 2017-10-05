---
title: "Tutorial: integración de Azure Active Directory con SAP NetWeaver | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: ad4140eb1183094a67822ad92eabcd35101360b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="9185b-103">Tutorial: Integración de Azure Active Directory con SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9185b-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="9185b-104">En este tutorial, aprenderá a integrar SAP NetWeaver con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9185b-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9185b-105">La integración de SAP NetWeaver con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9185b-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9185b-106">Puede controlar en Azure AD quién tiene acceso a SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9185b-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="9185b-107">Puede permitir que los usuarios inicien sesión automáticamente en SAP NetWeaver (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9185b-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9185b-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9185b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9185b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9185b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9185b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9185b-110">Prerequisites</span></span>

<span data-ttu-id="9185b-111">Para configurar la integración de Azure AD con SAP NetWeaver, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9185b-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="9185b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9185b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9185b-113">Una suscripción habilitada para el inicio de sesión único en SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9185b-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9185b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9185b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9185b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9185b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9185b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9185b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9185b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9185b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9185b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9185b-118">Scenario description</span></span>
<span data-ttu-id="9185b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9185b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9185b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9185b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9185b-121">Adición de SAP NetWeaver desde la galería</span><span class="sxs-lookup"><span data-stu-id="9185b-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="9185b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9185b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="9185b-123">Adición de SAP NetWeaver desde la galería</span><span class="sxs-lookup"><span data-stu-id="9185b-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="9185b-124">Para configurar la integración de SAP NetWeaver en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9185b-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9185b-125">**Para agregar SAP NetWeaver desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9185b-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9185b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9185b-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9185b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9185b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9185b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9185b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9185b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9185b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9185b-133">En el cuadro de búsqueda, escriba **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="9185b-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="9185b-135">En el panel de resultados, seleccione **SAP NetWeaver** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9185b-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9185b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9185b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9185b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SAP NetWeaver utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9185b-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9185b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SAP NetWeaver para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9185b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="9185b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9185b-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="9185b-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario** en SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9185b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="9185b-142">Para configurar y probar el inicio de sesión único de Azure AD con SAP NetWeaver, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9185b-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9185b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9185b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9185b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9185b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9185b-145">**[Creación de un usuario de prueba de SAP NetWeaver](#creating-an-sap-netweaver-test-user)**: el objetivo es tener un homólogo de Britta Simon en SAP NetWeaver que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9185b-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9185b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9185b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9185b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9185b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9185b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9185b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9185b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9185b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="9185b-150">**Para configurar el inicio de sesión único de Azure AD con SAP NetWeaver, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9185b-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="9185b-151">En la página de integración de la aplicación **SAP NetWeaver** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9185b-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9185b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9185b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="9185b-155">En la sección **Dominio y direcciones URL de SAP NetWeaver**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9185b-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="9185b-157">a.</span><span class="sxs-lookup"><span data-stu-id="9185b-157">a.</span></span> <span data-ttu-id="9185b-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<your company instance of SAP NetWeaver>`.</span><span class="sxs-lookup"><span data-stu-id="9185b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="9185b-159">b.</span><span class="sxs-lookup"><span data-stu-id="9185b-159">b.</span></span> <span data-ttu-id="9185b-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="9185b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="9185b-161">c.</span><span class="sxs-lookup"><span data-stu-id="9185b-161">c.</span></span> <span data-ttu-id="9185b-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`.</span><span class="sxs-lookup"><span data-stu-id="9185b-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9185b-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9185b-163">These values are not the real.</span></span> <span data-ttu-id="9185b-164">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9185b-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="9185b-165">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="9185b-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="9185b-166">Póngase en contacto con el [equipo de soporte técnico de SAP NetWeaver](https://www.sap.com/support.html) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9185b-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

4. <span data-ttu-id="9185b-167">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9185b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="9185b-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9185b-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="9185b-171">En la sección **Configuración de SAP NetWeaver**, haga clic en **Configurar SAP NetWeaver** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="9185b-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9185b-172">Copie el **id. de entidad de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="9185b-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="9185b-174">Para configurar el inicio de sesión único en **SAP NetWeaver**, debe enviar el **XML de metadatos** y el **id. de entidad de SAML** al [soporte técnico de SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="9185b-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="9185b-175">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9185b-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9185b-176">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9185b-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9185b-177">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9185b-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9185b-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9185b-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="9185b-179">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9185b-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9185b-181">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9185b-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9185b-182">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9185b-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9185b-184">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9185b-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9185b-186">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9185b-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9185b-188">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9185b-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9185b-190">a.</span><span class="sxs-lookup"><span data-stu-id="9185b-190">a.</span></span> <span data-ttu-id="9185b-191">En el cuadro de texto **Nombre**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9185b-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="9185b-192">b.</span><span class="sxs-lookup"><span data-stu-id="9185b-192">b.</span></span> <span data-ttu-id="9185b-193">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9185b-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="9185b-194">c.</span><span class="sxs-lookup"><span data-stu-id="9185b-194">c.</span></span> <span data-ttu-id="9185b-195">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9185b-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9185b-196">d.</span><span class="sxs-lookup"><span data-stu-id="9185b-196">d.</span></span> <span data-ttu-id="9185b-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9185b-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="9185b-198">Creación de un usuario de prueba de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9185b-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="9185b-199">En esta sección, creará un usuario llamado Britta Simon en SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9185b-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="9185b-200">Colabore con el [soporte técnico de SAP NetWeaver](https://www.sap.com/support.html) para agregar los usuarios de esta plataforma.</span><span class="sxs-lookup"><span data-stu-id="9185b-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9185b-201">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9185b-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9185b-202">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9185b-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9185b-204">**Para asignar el usuario Britta Simon a SAP NetWeaver, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9185b-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="9185b-205">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9185b-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9185b-207">En la lista de aplicaciones, seleccione **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="9185b-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="9185b-209">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9185b-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9185b-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9185b-211">Click **Add** button.</span></span> <span data-ttu-id="9185b-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9185b-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9185b-214">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9185b-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9185b-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9185b-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9185b-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9185b-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9185b-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9185b-217">Testing single sign-on</span></span>

<span data-ttu-id="9185b-218">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9185b-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9185b-219">Al hacer clic en el icono de SAP NetWeaver del panel de acceso, debería iniciar sesión automáticamente en la aplicación SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9185b-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9185b-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9185b-220">Additional resources</span></span>

* [<span data-ttu-id="9185b-221">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9185b-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9185b-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9185b-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

