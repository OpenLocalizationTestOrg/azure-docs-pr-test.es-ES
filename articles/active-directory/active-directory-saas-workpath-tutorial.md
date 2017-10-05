---
title: "Tutorial: integración de Azure Active Directory con Workpath | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="acde4-103">Tutorial: integración de Azure Active Directory con Workpath</span><span class="sxs-lookup"><span data-stu-id="acde4-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="acde4-104">En este tutorial, aprenderá a integrar Workpath con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acde4-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acde4-105">La integración de Workpath con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="acde4-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="acde4-106">En Azure AD puede controlar quién tiene acceso a Workpath</span><span class="sxs-lookup"><span data-stu-id="acde4-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="acde4-107">Puede permitir que los usuarios inicien sesión automáticamente en Workpath (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acde4-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="acde4-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="acde4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="acde4-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="acde4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acde4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="acde4-110">Prerequisites</span></span>

<span data-ttu-id="acde4-111">Para configurar la integración de Azure AD con Workpath, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="acde4-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="acde4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acde4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acde4-113">Una suscripción habilitada para el inicio de sesión único en Workpath</span><span class="sxs-lookup"><span data-stu-id="acde4-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acde4-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="acde4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acde4-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="acde4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acde4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="acde4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acde4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acde4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acde4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="acde4-118">Scenario description</span></span>
<span data-ttu-id="acde4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="acde4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acde4-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="acde4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acde4-121">Adición de Workpath desde la galería</span><span class="sxs-lookup"><span data-stu-id="acde4-121">Adding Workpath from the gallery</span></span>
2. <span data-ttu-id="acde4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acde4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="acde4-123">Adición de Workpath desde la galería</span><span class="sxs-lookup"><span data-stu-id="acde4-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="acde4-124">Para configurar la integración de Workpath en Azure AD, será preciso que agregue Workpath desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="acde4-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="acde4-125">**Para agregar Workpath desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="acde4-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="acde4-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acde4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="acde4-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="acde4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="acde4-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="acde4-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="acde4-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="acde4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="acde4-133">En el cuadro de búsqueda, escriba **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="acde4-133">In the search box, type **Workpath**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="acde4-135">En el panel de resultados, seleccione **Workpath** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acde4-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="acde4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acde4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="acde4-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Workpath con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="acde4-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="acde4-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Workpath para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acde4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="acde4-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Workpath.</span><span class="sxs-lookup"><span data-stu-id="acde4-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="acde4-141">En Workpath, para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="acde4-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="acde4-142">Para configurar y probar el inicio de sesión único de Azure AD con Workpath, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="acde4-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="acde4-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="acde4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="acde4-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acde4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="acde4-145">**[Creación de un usuario de prueba de Workpath](#creating-a-workpath-test-user)**: para tener un homólogo de Britta Simon en Workpath que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acde4-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="acde4-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acde4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acde4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="acde4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="acde4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acde4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="acde4-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Workpath.</span><span class="sxs-lookup"><span data-stu-id="acde4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="acde4-150">**Para configurar el inicio de sesión único de Azure AD con Workpath, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="acde4-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="acde4-151">En Azure Portal, en la página de integración de la aplicación **Workpath**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="acde4-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="acde4-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="acde4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="acde4-155">En la sección **Dominio y direcciones URL de Workpath**, si quiere configurar la aplicación en modo iniciado por **IDP**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="acde4-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="acde4-157">a.</span><span class="sxs-lookup"><span data-stu-id="acde4-157">a.</span></span> <span data-ttu-id="acde4-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="acde4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="acde4-159">b.</span><span class="sxs-lookup"><span data-stu-id="acde4-159">b.</span></span> <span data-ttu-id="acde4-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://api.workpath.com/v1/saml/assert/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="acde4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="acde4-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="acde4-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="acde4-162">Si desea configurar la aplicación en modo iniciado por **SP**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="acde4-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="acde4-164">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.workpath.com/ `.</span><span class="sxs-lookup"><span data-stu-id="acde4-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="acde4-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="acde4-165">These values are not real.</span></span> <span data-ttu-id="acde4-166">Actualícelos con la dirección URL de inicio de sesión, el identificador y la dirección URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="acde4-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="acde4-167">Póngase en contacto con el [equipo de soporte técnico de Workpath](https://help.workpath.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="acde4-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

5. <span data-ttu-id="acde4-168">La aplicación Workpath espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="acde4-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="acde4-169">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="acde4-169">Configure the following claims for this application.</span></span> <span data-ttu-id="acde4-170">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="acde4-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="acde4-171">En la siguiente captura de pantalla se muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="acde4-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="acde4-173">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="acde4-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="acde4-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="acde4-174">Attribute Name</span></span> | <span data-ttu-id="acde4-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="acde4-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="acde4-176">first_name</span><span class="sxs-lookup"><span data-stu-id="acde4-176">first_name</span></span> | <span data-ttu-id="acde4-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="acde4-177">user.givenname</span></span> |
    | <span data-ttu-id="acde4-178">last_name</span><span class="sxs-lookup"><span data-stu-id="acde4-178">last_name</span></span> | <span data-ttu-id="acde4-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="acde4-179">user.surname</span></span> |
    
    <span data-ttu-id="acde4-180">a.</span><span class="sxs-lookup"><span data-stu-id="acde4-180">a.</span></span> <span data-ttu-id="acde4-181">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="acde4-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="acde4-183">b.</span><span class="sxs-lookup"><span data-stu-id="acde4-183">b.</span></span> <span data-ttu-id="acde4-184">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="acde4-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="acde4-186">c.</span><span class="sxs-lookup"><span data-stu-id="acde4-186">c.</span></span> <span data-ttu-id="acde4-187">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="acde4-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="acde4-188">d.</span><span class="sxs-lookup"><span data-stu-id="acde4-188">d.</span></span> <span data-ttu-id="acde4-189">Deje el cuadro de texto **Espacio de nombres** en blanco.</span><span class="sxs-lookup"><span data-stu-id="acde4-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="acde4-190">e.</span><span class="sxs-lookup"><span data-stu-id="acde4-190">e.</span></span> <span data-ttu-id="acde4-191">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="acde4-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="acde4-192">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="acde4-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="acde4-194">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="acde4-194">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="acde4-196">En la sección **Configuración de Workpath**, haga clic en **Configurar Workpath** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="acde4-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="acde4-197">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="acde4-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="acde4-199">Para configurar el inicio de sesión único en **Workpath**, es preciso enviar los valores descargados de **XML de metadatos**, **Dirección URL de cierre de sesión, SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="acde4-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="acde4-200">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acde4-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="acde4-201">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="acde4-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="acde4-202">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="acde4-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="acde4-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acde4-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="acde4-204">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="acde4-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="acde4-206">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="acde4-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="acde4-207">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acde4-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="acde4-209">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="acde4-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="acde4-211">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="acde4-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="acde4-213">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="acde4-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="acde4-215">a.</span><span class="sxs-lookup"><span data-stu-id="acde4-215">a.</span></span> <span data-ttu-id="acde4-216">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="acde4-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acde4-217">b.</span><span class="sxs-lookup"><span data-stu-id="acde4-217">b.</span></span> <span data-ttu-id="acde4-218">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acde4-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="acde4-219">c.</span><span class="sxs-lookup"><span data-stu-id="acde4-219">c.</span></span> <span data-ttu-id="acde4-220">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="acde4-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="acde4-221">d.</span><span class="sxs-lookup"><span data-stu-id="acde4-221">d.</span></span> <span data-ttu-id="acde4-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="acde4-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="acde4-223">Creación de un usuario de prueba de Workpath</span><span class="sxs-lookup"><span data-stu-id="acde4-223">Creating a Workpath test user</span></span>

<span data-ttu-id="acde4-224">Workpath admite aprovisionamiento de usuarios Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="acde4-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="acde4-225">Después se crean usuarios de autenticación en la aplicación automáticamente.</span><span class="sxs-lookup"><span data-stu-id="acde4-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="acde4-226">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="acde4-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="acde4-227">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Workpath.</span><span class="sxs-lookup"><span data-stu-id="acde4-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="acde4-229">**Para asignar Britta Simon a Workpath, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="acde4-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="acde4-230">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="acde4-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="acde4-232">En la lista de aplicaciones, seleccione **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="acde4-232">In the applications list, select **Workpath**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="acde4-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="acde4-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="acde4-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="acde4-236">Click **Add** button.</span></span> <span data-ttu-id="acde4-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="acde4-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="acde4-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="acde4-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="acde4-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="acde4-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acde4-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="acde4-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="acde4-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="acde4-242">Testing single sign-on</span></span>

<span data-ttu-id="acde4-243">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="acde4-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="acde4-244">Al hacer clic en el icono de Workpath en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Workpath.</span><span class="sxs-lookup"><span data-stu-id="acde4-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="acde4-245">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="acde4-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="acde4-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="acde4-246">Additional resources</span></span>

* [<span data-ttu-id="acde4-247">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acde4-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acde4-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="acde4-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

