---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform Identity Authentication | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SAP HANA Cloud Platform Identity Authentication."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="439fa-103">Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="439fa-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="439fa-104">En este tutorial, aprenderá a integrar SAP HANA Cloud Platform Identity Authentication con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="439fa-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="439fa-105">SAP HANA Cloud Platform Identity Authentication se utiliza como IdP de proxy para obtener acceso a las aplicaciones de SAP con Azure AD como IdP principal.</span><span class="sxs-lookup"><span data-stu-id="439fa-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="439fa-106">La integración de SAP HANA Cloud Platform Identity Authentication con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="439fa-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="439fa-107">En Azure AD puede controlar quién tiene acceso a la aplicación de SAP.</span><span class="sxs-lookup"><span data-stu-id="439fa-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="439fa-108">Puede permitir que los usuarios inicien sesión automáticamente en aplicaciones de SAP (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="439fa-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="439fa-109">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="439fa-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="439fa-110">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="439fa-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="439fa-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="439fa-111">Prerequisites</span></span>

<span data-ttu-id="439fa-112">Para configurar la integración de Azure AD con SAP HANA Cloud Platform Identity Authentication, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="439fa-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="439fa-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="439fa-113">An Azure AD subscription</span></span>
- <span data-ttu-id="439fa-114">Una suscripción de **SAP HANA Cloud Platform Identity Authentication** con el inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="439fa-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="439fa-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="439fa-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="439fa-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="439fa-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="439fa-117">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="439fa-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="439fa-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="439fa-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="439fa-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="439fa-119">Scenario description</span></span>
<span data-ttu-id="439fa-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="439fa-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="439fa-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="439fa-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="439fa-122">Incorporación de SAP HANA Cloud Platform Identity Authentication desde la galería</span><span class="sxs-lookup"><span data-stu-id="439fa-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="439fa-123">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="439fa-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="439fa-124">Antes de adentrarnos en los detalles técnicos, es fundamental entender los conceptos vamos a tratar.</span><span class="sxs-lookup"><span data-stu-id="439fa-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="439fa-125">La federación de Azure Active Directory y SAP HANA Cloud Platform Identity Authentication le permite implementar el inicio de sesión único en aplicaciones o servicios protegidos por AAD (como un IdP) con aplicaciones y servicios de SAP protegidos por SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="439fa-126">Actualmente, SAP HANA Cloud Platform Identity Authentication actúa como un proveedor de identidades de proxy en las aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="439fa-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="439fa-127">A su vez, Azure Active Directory funciona como el proveedor de identidades principal en esta configuración.</span><span class="sxs-lookup"><span data-stu-id="439fa-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="439fa-128">El siguiente diagrama lo muestra:</span><span class="sxs-lookup"><span data-stu-id="439fa-128">The following diagram illustrates this:</span></span>    

![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="439fa-130">Con esta configuración, su inquilino de SAP HANA Cloud Platform Identity Authentication se configurará como una aplicación de confianza en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="439fa-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="439fa-131">Todos los servicios y las aplicaciones de SAP que desea proteger de esta manera se configuran posteriormente en la consola de administración de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="439fa-132">Es decir, para llevar a cabo este proceso de configuración, la autorización de concesión de acceso a servicios y aplicaciones de SAP debe realizarse en SAP HANA Cloud Platform Identity Authentication (en lugar de en Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="439fa-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="439fa-133">Si se configura SAP HANA Cloud Platform Identity Authentication como una aplicación a través de Azure Active Directory Marketplace, no hay que ajustar las notificaciones ni las transformaciones y aserciones de SAML necesarias para producir un token de autenticación válido para las aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="439fa-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="439fa-134">Actualmente, el SSO web solo se ha probado en ambas soluciones.</span><span class="sxs-lookup"><span data-stu-id="439fa-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="439fa-135">Aunque los flujos necesarios para establecer comunicación de aplicación a API o de API a API deberían funcionar, todavía no se han probado.</span><span class="sxs-lookup"><span data-stu-id="439fa-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="439fa-136">Sin embargo, sí que se hará en actividades posteriores.</span><span class="sxs-lookup"><span data-stu-id="439fa-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="439fa-137">Agregar SAP HANA Cloud Platform Identity Authentication desde la galería</span><span class="sxs-lookup"><span data-stu-id="439fa-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="439fa-138">Para configurar la integración de SAP HANA Cloud Platform Identity Authentication en Azure AD, debe agregar SAP HANA Cloud Platform Identity Authentication desde la galería a la lista de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="439fa-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="439fa-139">**Para agregar SAP HANA Cloud Platform Identity Authentication desde la galería, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="439fa-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="439fa-140">En el panel de navegación izquierdo del [**Portal de administración de Azure**](https://portal.azure.com), haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="439fa-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="439fa-142">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="439fa-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="439fa-143">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="439fa-143">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="439fa-145">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="439fa-145">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="439fa-147">En el cuadro de búsqueda, escriba **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="439fa-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="439fa-149">En el panel de resultados, seleccione **SAP HANA Cloud Platform Identity Authentication**y, luego, haga clic en el botón **Agregar** para incorporar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="439fa-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="439fa-151">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="439fa-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="439fa-152">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con SAP HANA Cloud Platform Identity Authentication con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="439fa-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="439fa-153">Para que el inicio de sesión único funcione, es preciso que Azure AD sepa cuál es el usuario homólogo de SAP HANA Cloud Platform Identity Authentication para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="439fa-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="439fa-154">Es decir, hay que establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="439fa-155">Esta relación de vínculo se establece asignando el valor del **nombre de usuario** de Azure AD como el del **nombre de usuario** de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="439fa-156">Para configurar y probar el inicio de sesión único de Azure AD con SAP HANA Cloud Platform Identity Authentication, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="439fa-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="439fa-157">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)**: para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="439fa-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="439fa-158">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="439fa-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="439fa-159">**[Creación de un usuario de SAP HANA Cloud Platform Identity Authentication](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**: para tener un equivalente de Britta Simon en SAP HANA Cloud Platform Identity Authentication que esté vinculado a su representación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="439fa-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="439fa-160">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="439fa-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="439fa-161">**[Prueba del inicio de sesión único](#testing-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="439fa-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="439fa-162">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="439fa-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="439fa-163">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="439fa-164">La aplicación SAP HANA Cloud Platform Identity Authentication espera las aserciones de SAML con un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="439fa-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="439fa-165">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="439fa-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="439fa-166">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="439fa-166">The following screenshot shows an example for this.</span></span>

![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="439fa-168">**Para configurar el inicio de sesión único de Azure AD con SAP HANA Cloud Platform Identity Authentication, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="439fa-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="439fa-169">En el Portal de administración de Azure, en la página de integración de la aplicación **SAP HANA Cloud Platform Identity Authentication**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="439fa-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="439fa-171">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="439fa-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único][5]

3. <span data-ttu-id="439fa-173">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, si la aplicación de SAP espera un atributo, por ejemplo, "firstName".</span><span class="sxs-lookup"><span data-stu-id="439fa-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="439fa-174">En el cuadro de diálogo Atributos de token de SAML, agregue el atributo "firstName".</span><span class="sxs-lookup"><span data-stu-id="439fa-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="439fa-175">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="439fa-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![Configurar inicio de sesión único][6]

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="439fa-178">En el cuadro de texto **Nombre de atributo**, escriba el nombre de atributo "firstName".</span><span class="sxs-lookup"><span data-stu-id="439fa-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="439fa-179">En la lista **Valor de atributo**, seleccione el valor de atributo "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="439fa-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="439fa-180">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="439fa-180">Click **Ok**.</span></span>

4. <span data-ttu-id="439fa-181">En la sección **Dominio y direcciones URL de SAP HANA Cloud Platform Identity Authentication**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="439fa-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="439fa-183">En el cuadro de texto **URL de inicio de sesión**, escriba la URL de inicio de sesión de la aplicación de SAP.</span><span class="sxs-lookup"><span data-stu-id="439fa-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="439fa-184">En el cuadro de texto **Identificador**, escriba el valor con el siguiente patrón: `<entity-id>.accounts.ondemand.com`.</span><span class="sxs-lookup"><span data-stu-id="439fa-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="439fa-185">Si no conoce este valor, siga la documentación de SAP HANA Cloud Platform Identity Authentication; en concreto, el capítulo de [Configuración de inquilino de SAML 2.0](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)</span><span class="sxs-lookup"><span data-stu-id="439fa-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="439fa-186">En la sección **Configuración de SAP HANA Cloud Platform Identity Authentication**, haga clic en **Configurar SAP HANA Cloud Platform Identity Authentication** para abrir el cuadro de diálogo **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="439fa-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="439fa-187">Luego, haga clic en **SAML XML Metadata** (Metadatos XML de SAML) y guarde el archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="439fa-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="439fa-190">Para configurar el SSO en su aplicación, vaya a la consola de administración de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="439fa-191">La dirección URL tiene el siguiente patrón: `https://<tenant-id>.accounts.ondemand.com/admin`.</span><span class="sxs-lookup"><span data-stu-id="439fa-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="439fa-192">Después, siga la documentación de SAP HANA Cloud Platform Identity Authentication para [Configurar Microsoft Azure AD como proveedor de identidades corporativas en SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="439fa-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="439fa-193">En el Portal de administración de Azure, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="439fa-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="439fa-194">Siga los pasos siguientes solo si desea agregar y habilitar SSO para otra aplicación de SAP.</span><span class="sxs-lookup"><span data-stu-id="439fa-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="439fa-195">Repita los pasos de la sección "Incorporación de SAP HANA Cloud Platform Identity Authentication desde la galería" para agregar otra instancia de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="439fa-196">En el Portal de administración de Azure, en la página de integración de la aplicación **SAP HANA Cloud Platform Identity Authentication**, haga clic en **Inicio de sesión vinculado**.</span><span class="sxs-lookup"><span data-stu-id="439fa-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configuración del inicio de sesión vinculado](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="439fa-198">Luego, guarde la configuración.</span><span class="sxs-lookup"><span data-stu-id="439fa-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="439fa-199">La nueva aplicación usará la configuración de SSO para la aplicación de SAP anterior.</span><span class="sxs-lookup"><span data-stu-id="439fa-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="439fa-200">Asegúrese de usar los mismos proveedores de identidades corporativas en la consola de administración de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="439fa-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="439fa-201">Create an Azure AD test user</span></span>
<span data-ttu-id="439fa-202">El objetivo de esta sección es crear un usuario de prueba en el nuevo portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="439fa-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="439fa-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="439fa-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="439fa-205">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="439fa-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="439fa-207">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="439fa-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="439fa-209">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="439fa-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="439fa-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="439fa-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="439fa-213">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="439fa-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="439fa-214">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="439fa-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="439fa-215">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="439fa-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="439fa-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="439fa-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="439fa-217">Creación de un usuario de prueba de SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="439fa-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="439fa-218">No hace falta crear un usuario en SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="439fa-219">Los usuarios que están en el almacén de usuarios de Azure AD pueden utilizar la funcionalidad de inicio de sesión único (SSO).</span><span class="sxs-lookup"><span data-stu-id="439fa-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="439fa-220">SAP HANA Cloud Platform Identity Authentication es compatible con la opción de federación de identidades.</span><span class="sxs-lookup"><span data-stu-id="439fa-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="439fa-221">Esta opción permite a la aplicación comprobar si los usuarios autenticados mediante el proveedor de identidades corporativas se encuentran en el almacén de usuarios de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="439fa-222">En la configuración predeterminada, la opción de federación de identidades está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="439fa-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="439fa-223">Si se habilita, solo los usuarios que se importan de SAP HANA Cloud Platform Identity Authentication pueden tener acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="439fa-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="439fa-224">Para más información sobre cómo habilitar o deshabilitar la federación de identidades con SAP HANA Cloud Platform Identity Authentication, consulte la sección Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication (Activación de la federación de identidades con SAP HANA Cloud Platform Identity Authentication) del artículo [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html) (Configuración de la federación de identidades con el almacén de usuarios de SAP HANA Cloud Platform Identity Authentication).</span><span class="sxs-lookup"><span data-stu-id="439fa-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="439fa-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="439fa-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="439fa-226">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="439fa-228">**Para asignar Britta Simon a SAP HANA Cloud Platform Identity Authentication, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="439fa-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="439fa-229">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y seleccione **Aplicaciones empresariales**. Después, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="439fa-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="439fa-231">En la lista de aplicaciones, seleccione **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="439fa-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="439fa-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="439fa-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="439fa-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="439fa-235">Click **Add** button.</span></span> <span data-ttu-id="439fa-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="439fa-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="439fa-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="439fa-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="439fa-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="439fa-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="439fa-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="439fa-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="439fa-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="439fa-241">Test single sign-on</span></span>

<span data-ttu-id="439fa-242">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="439fa-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="439fa-243">Al hacer clic en el icono de SAP HANA Cloud Platform Identity Authentication del panel de acceso, debe iniciar sesión automáticamente en su aplicación SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="439fa-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="439fa-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="439fa-244">Additional resources</span></span>

* [<span data-ttu-id="439fa-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="439fa-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="439fa-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="439fa-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png