---
title: "Tutorial: Integración de Azure Active Directory con AirWatch | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="b69c2-103">Tutorial: Integración de Azure Active Directory con AirWatch</span><span class="sxs-lookup"><span data-stu-id="b69c2-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="b69c2-104">En este tutorial, aprenderá a integrar AirWatch con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b69c2-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b69c2-105">La integración de AirWatch con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b69c2-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b69c2-106">Puede controlar en Azure AD quién tiene acceso a AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b69c2-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="b69c2-107">Puede permitir que los usuarios inicien sesión automáticamente en AirWatch (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b69c2-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b69c2-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b69c2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b69c2-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b69c2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b69c2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b69c2-110">Prerequisites</span></span>

<span data-ttu-id="b69c2-111">Para configurar la integración de Azure AD con AirWatch, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b69c2-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="b69c2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b69c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b69c2-113">Una suscripción habilitada para el inicio de sesión único en AirWatch</span><span class="sxs-lookup"><span data-stu-id="b69c2-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b69c2-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b69c2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b69c2-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b69c2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b69c2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b69c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b69c2-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b69c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b69c2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b69c2-118">Scenario description</span></span>
<span data-ttu-id="b69c2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b69c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b69c2-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b69c2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b69c2-121">Incorporación de AirWatch desde la Galería</span><span class="sxs-lookup"><span data-stu-id="b69c2-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="b69c2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b69c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="b69c2-123">Incorporación de AirWatch desde la Galería</span><span class="sxs-lookup"><span data-stu-id="b69c2-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="b69c2-124">Para configurar la integración de AirWatch en Azure AD, es preciso agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b69c2-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b69c2-125">**Para agregar AirWatch desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b69c2-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b69c2-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b69c2-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b69c2-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b69c2-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b69c2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b69c2-133">En el cuadro de búsqueda, escriba **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-133">In the search box, type **AirWatch**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="b69c2-135">En el panel de resultados, seleccione **AirWatch** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b69c2-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b69c2-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b69c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b69c2-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AirWatch con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b69c2-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b69c2-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de AirWatch para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b69c2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="b69c2-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b69c2-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="b69c2-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como valor de **Nombre de usuario** en AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b69c2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="b69c2-142">Para configurar y probar el inicio de sesión único de Azure AD con AirWatch, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b69c2-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b69c2-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b69c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b69c2-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b69c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b69c2-145">**[Creación de un usuario de prueba de AirWatch](#creating-a-airwatch-test-user)**: para tener un homólogo de Britta Simon en AirWatch vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b69c2-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b69c2-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b69c2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b69c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b69c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b69c2-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b69c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b69c2-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b69c2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="b69c2-150">**Para configurar el inicio de sesión único de Azure AD con AirWatch, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b69c2-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="b69c2-151">En Azure Portal, en la página de integración de la aplicación **AirWatch**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b69c2-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b69c2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="b69c2-155">En la sección **AirWatch Domain and URLs** (Dominios y direcciones URL de AirWatch), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b69c2-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="b69c2-157">a.</span><span class="sxs-lookup"><span data-stu-id="b69c2-157">a.</span></span> <span data-ttu-id="b69c2-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`.</span><span class="sxs-lookup"><span data-stu-id="b69c2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="b69c2-159">b.</span><span class="sxs-lookup"><span data-stu-id="b69c2-159">b.</span></span> <span data-ttu-id="b69c2-160">En el cuadro de texto **Identificador**, escriba el valor como `AirWatch`.</span><span class="sxs-lookup"><span data-stu-id="b69c2-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b69c2-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="b69c2-161">This value is not the real.</span></span> <span data-ttu-id="b69c2-162">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="b69c2-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="b69c2-163">Póngase en contacto con el [equipo de soporte técnico de AirWatch](http://www.air-watch.com/company/contact-us/) para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="b69c2-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="b69c2-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b69c2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="b69c2-166">En la sección **AirWatch Configuration** (Configuración de AirWatch), haga clic en **Configure AirWatch** (Configurar AirWatch) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b69c2-167">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="b69c2-169">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-169">Click **Save** button.</span></span>

    <span data-ttu-id="b69c2-170">![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="b69c2-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="b69c2-171">En otra ventana del explorador web, inicie sesión en el sitio de AirWatch de la compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="b69c2-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="b69c2-172">En el panel de navegación izquierdo, haga clic en **Accounts** (Cuentas) y, luego, en **Administrators** (Administradores).</span><span class="sxs-lookup"><span data-stu-id="b69c2-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="b69c2-173">![Administradores](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administradores")</span><span class="sxs-lookup"><span data-stu-id="b69c2-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="b69c2-174">Expanda el menú **Settings** (Configuración) y, a continuación, haga clic en **Directory Services** (Servicios de directorio).</span><span class="sxs-lookup"><span data-stu-id="b69c2-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="b69c2-175">![Configuración](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="b69c2-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="b69c2-176">Haga clic en la pestaña **Usuario**; en el cuadro de texto **DN base**, escriba el nombre de dominio y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="b69c2-177">![Usuario](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="b69c2-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="b69c2-178">Haga clic en la pestaña **Server** (Servidor).</span><span class="sxs-lookup"><span data-stu-id="b69c2-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="b69c2-179">![Servidor](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Servidor")</span><span class="sxs-lookup"><span data-stu-id="b69c2-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="b69c2-180">Lleve a cabo los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="b69c2-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="b69c2-181">![Cargar](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Cargar")</span><span class="sxs-lookup"><span data-stu-id="b69c2-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="b69c2-182">a.</span><span class="sxs-lookup"><span data-stu-id="b69c2-182">a.</span></span> <span data-ttu-id="b69c2-183">En **Directory Type** (Tipo de directorio), seleccione **None** (Ninguno).</span><span class="sxs-lookup"><span data-stu-id="b69c2-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="b69c2-184">b.</span><span class="sxs-lookup"><span data-stu-id="b69c2-184">b.</span></span> <span data-ttu-id="b69c2-185">Seleccione **Use SAML For Authentication**(Usar SAML para autenticación).</span><span class="sxs-lookup"><span data-stu-id="b69c2-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="b69c2-186">c.</span><span class="sxs-lookup"><span data-stu-id="b69c2-186">c.</span></span> <span data-ttu-id="b69c2-187">Para cargar el certificado descargado, haga clic en **Upload**(Cargar).</span><span class="sxs-lookup"><span data-stu-id="b69c2-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="b69c2-188">En la sección **Request** (Solicitud), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b69c2-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="b69c2-189">![Solicitud](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Solicitud")</span><span class="sxs-lookup"><span data-stu-id="b69c2-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="b69c2-190">a.</span><span class="sxs-lookup"><span data-stu-id="b69c2-190">a.</span></span> <span data-ttu-id="b69c2-191">En **Request Binding Type** (Tipo de enlace de solicitud), seleccione **POST**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="b69c2-192">b.</span><span class="sxs-lookup"><span data-stu-id="b69c2-192">b.</span></span> <span data-ttu-id="b69c2-193">En Azure Portal, en la página de diálogo **Configure single sign-on at Airwatch** (Configurar inicio de sesión único en Airwatch), copie el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) y péguelo en el cuadro de texto **Identity Provider Single Sign On URL** (Dirección URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="b69c2-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="b69c2-194">c.</span><span class="sxs-lookup"><span data-stu-id="b69c2-194">c.</span></span> <span data-ttu-id="b69c2-195">En la lista **NameID Format** (Formato de NameID), seleccione **Email address** (Dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="b69c2-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="b69c2-196">d.</span><span class="sxs-lookup"><span data-stu-id="b69c2-196">d.</span></span> <span data-ttu-id="b69c2-197">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-197">Click **Save**.</span></span>

14. <span data-ttu-id="b69c2-198">Haga clic de nuevo en la pestaña **User** (Usuario).</span><span class="sxs-lookup"><span data-stu-id="b69c2-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="b69c2-199">![Usuario](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="b69c2-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="b69c2-200">En la sección **Attribute** (Atributo), realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b69c2-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="b69c2-201">![Atributo](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Atributo")</span><span class="sxs-lookup"><span data-stu-id="b69c2-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="b69c2-202">a.</span><span class="sxs-lookup"><span data-stu-id="b69c2-202">a.</span></span> <span data-ttu-id="b69c2-203">En el cuadro de texto **Identificador de objeto**, escriba **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="b69c2-204">b.</span><span class="sxs-lookup"><span data-stu-id="b69c2-204">b.</span></span> <span data-ttu-id="b69c2-205">En el cuadro de texto **Nombre de usuario**, escriba **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="b69c2-206">c.</span><span class="sxs-lookup"><span data-stu-id="b69c2-206">c.</span></span> <span data-ttu-id="b69c2-207">En el cuadro de texto **Nombre para mostrar**, escriba **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="b69c2-208">d.</span><span class="sxs-lookup"><span data-stu-id="b69c2-208">d.</span></span> <span data-ttu-id="b69c2-209">En el cuadro de texto **Nombre**, escriba **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="b69c2-210">e.</span><span class="sxs-lookup"><span data-stu-id="b69c2-210">e.</span></span> <span data-ttu-id="b69c2-211">En el cuadro de texto **Apellidos**, escriba **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="b69c2-212">f.</span><span class="sxs-lookup"><span data-stu-id="b69c2-212">f.</span></span> <span data-ttu-id="b69c2-213">En el cuadro de texto **Correo electrónico**, escriba **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="b69c2-214">g.</span><span class="sxs-lookup"><span data-stu-id="b69c2-214">g.</span></span> <span data-ttu-id="b69c2-215">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b69c2-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b69c2-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="b69c2-217">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b69c2-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b69c2-219">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b69c2-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b69c2-220">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b69c2-222">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b69c2-224">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b69c2-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b69c2-226">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b69c2-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b69c2-228">a.</span><span class="sxs-lookup"><span data-stu-id="b69c2-228">a.</span></span> <span data-ttu-id="b69c2-229">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b69c2-230">b.</span><span class="sxs-lookup"><span data-stu-id="b69c2-230">b.</span></span> <span data-ttu-id="b69c2-231">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b69c2-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b69c2-232">c.</span><span class="sxs-lookup"><span data-stu-id="b69c2-232">c.</span></span> <span data-ttu-id="b69c2-233">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b69c2-234">d.</span><span class="sxs-lookup"><span data-stu-id="b69c2-234">d.</span></span> <span data-ttu-id="b69c2-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="b69c2-236">Creación de un usuario de prueba de AirWatch</span><span class="sxs-lookup"><span data-stu-id="b69c2-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="b69c2-237">Para permitir que los usuarios de Azure AD inicien sesión en AirWatch, tienen que aprovisionarse en AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b69c2-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="b69c2-238">En el caso de AirWatch, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="b69c2-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="b69c2-239">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="b69c2-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b69c2-240">Inicie sesión en el sitio de la compañía de **AirWatch** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b69c2-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="b69c2-241">En el panel de navegación izquierdo, haga clic en **Accounts** (Cuentas) y luego en **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="b69c2-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="b69c2-242">![Usuarios](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="b69c2-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="b69c2-243">En el menú **Users** (Usuarios), haga clic en **List View** (Vista de lista) y, a continuación, haga clic en **Add \> Add User** (Agregar > Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="b69c2-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="b69c2-244">![Agregar usuario](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="b69c2-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="b69c2-245">En el cuadro de diálogo **Add / Edit User** (Agregar/Editar usuario), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b69c2-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="b69c2-246">![Agregar usuario](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="b69c2-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="b69c2-247">Especifique **Username** (Nombre de usuario), **Password** (Contraseña), **Confirm Password** (Confirmar contraseña), **First Name** (Nombre), **Last Name** (Apellido), **Email Address** (Correo electrónico) de una cuenta de Azure Active Directory válida que quiera aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="b69c2-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="b69c2-248">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b69c2-249">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de AirWatch ofrecida por AirWatch para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="b69c2-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b69c2-250">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b69c2-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b69c2-251">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b69c2-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b69c2-253">**Para asignar Britta Simon a AirWatch, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b69c2-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="b69c2-254">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b69c2-256">En la lista de aplicaciones, seleccione **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-256">In the applications list, select **AirWatch**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="b69c2-258">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-258">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b69c2-260">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-260">Click **Add** button.</span></span> <span data-ttu-id="b69c2-261">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b69c2-263">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b69c2-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b69c2-264">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b69c2-265">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b69c2-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b69c2-266">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b69c2-266">Testing single sign-on</span></span>

<span data-ttu-id="b69c2-267">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b69c2-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b69c2-268">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b69c2-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b69c2-269">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b69c2-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b69c2-270">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b69c2-270">Additional resources</span></span>

* [<span data-ttu-id="b69c2-271">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b69c2-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b69c2-272">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b69c2-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

