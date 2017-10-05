---
title: "Tutorial: Integración de Azure Active Directory con ADP GlobalView | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y ADP GlobalView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="5eef0-103">Tutorial: Integración de Azure Active Directory con ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="5eef0-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="5eef0-104">En este tutorial, obtendrá información sobre cómo integrar ADP GlobalView con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5eef0-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5eef0-105">La integración de ADP GlobalView con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5eef0-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5eef0-106">En Azure AD puede controlar quién tiene acceso a ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="5eef0-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="5eef0-107">Puede permitir que los usuarios inicien sesión automáticamente en ADP GlobalView (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eef0-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5eef0-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5eef0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5eef0-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5eef0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eef0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5eef0-110">Prerequisites</span></span>

<span data-ttu-id="5eef0-111">Para configurar la integración de Azure AD con ADP GlobalView, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5eef0-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="5eef0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eef0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5eef0-113">Una suscripción habilitada para el inicio de sesión único en ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="5eef0-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5eef0-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5eef0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5eef0-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5eef0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5eef0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5eef0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5eef0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5eef0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5eef0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5eef0-118">Scenario description</span></span>
<span data-ttu-id="5eef0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5eef0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5eef0-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="5eef0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5eef0-121">Incorporación de ADP GlobalView desde la galería</span><span class="sxs-lookup"><span data-stu-id="5eef0-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="5eef0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eef0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="5eef0-123">Incorporación de ADP GlobalView desde la galería</span><span class="sxs-lookup"><span data-stu-id="5eef0-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="5eef0-124">Para configurar la integración de ADP GlobalView en Azure AD, es preciso agregar ADP GlobalView desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="5eef0-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5eef0-125">**Para agregar ADP GlobalView desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="5eef0-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5eef0-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5eef0-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5eef0-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5eef0-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5eef0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5eef0-133">En el cuadro de búsqueda, escriba **ADP GlobalView**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-133">In the search box, type **ADP Globalview**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="5eef0-135">En el panel de resultados, seleccione **ADP GlobalView** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5eef0-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5eef0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eef0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5eef0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ADP GlobalView con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5eef0-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5eef0-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ADP GlobalView para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5eef0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="5eef0-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="5eef0-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="5eef0-141">Para establecer la relación de vínculo, en ADP GlobalView, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="5eef0-142">Para configurar y probar el inicio de sesión único de Azure AD con ADP GlobalView, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5eef0-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5eef0-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="5eef0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5eef0-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5eef0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5eef0-145">**[Creación de un usuario de prueba de ADP GlobalView](#creating-an-adp-globalview-test-user)**: para tener un homólogo de Britta Simon en ADP GlobalView que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5eef0-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5eef0-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5eef0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5eef0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5eef0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5eef0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eef0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5eef0-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="5eef0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="5eef0-150">**Para configurar el inicio de sesión único de Azure AD con ADP GlobalView, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="5eef0-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="5eef0-151">En Azure Portal, en la página de integración de la aplicación **ADP GlobalView**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5eef0-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5eef0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="5eef0-155">En la sección **Dominio y direcciones URL de ADP GlobalView**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5eef0-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="5eef0-157">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.globalview.adp.com/federate` o `https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="5eef0-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5eef0-158">El valor no es real.</span><span class="sxs-lookup"><span data-stu-id="5eef0-158">The value is not real.</span></span> <span data-ttu-id="5eef0-159">Actualícelo con el identificador real.</span><span class="sxs-lookup"><span data-stu-id="5eef0-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="5eef0-160">Póngase en contacto con el [soporte técnico de ADP Globalview](https://www.adp.com/contact-us/overview.aspx) para obtener el valor.</span><span class="sxs-lookup"><span data-stu-id="5eef0-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="5eef0-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5eef0-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="5eef0-163">La aplicación ADP GlobalView espera las aserciones de SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="5eef0-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="5eef0-164">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="5eef0-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="5eef0-165">El nombre de la notificación siempre será **"PersonImmutableID"** cuyo valor hemos asignado a ExtensionAttribute2 que contiene el EmployeeID del usuario.</span><span class="sxs-lookup"><span data-stu-id="5eef0-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="5eef0-166">Aquí se realiza la asignación de usuario desde Azure AD a ADP GlobalView en el valor EmployeeID, pero puede asignarlo a un valor diferente que también se base en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5eef0-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="5eef0-167">Puede trabajar primero con el equipo de ADP GlobalView para usar el identificador correcto de un usuario y asignar ese valor con la notificación **"PersonImmutableID"**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="5eef0-168">También puede asignar la notificación Email y UserID como se muestra en la imagen.</span><span class="sxs-lookup"><span data-stu-id="5eef0-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="5eef0-170">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5eef0-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="5eef0-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="5eef0-171">Attribute Name</span></span> | <span data-ttu-id="5eef0-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="5eef0-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="5eef0-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="5eef0-173">personalimmutableid</span></span> | <span data-ttu-id="5eef0-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="5eef0-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="5eef0-175">email</span><span class="sxs-lookup"><span data-stu-id="5eef0-175">email</span></span>               | <span data-ttu-id="5eef0-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="5eef0-176">user.mail</span></span> |
    | <span data-ttu-id="5eef0-177">userid</span><span class="sxs-lookup"><span data-stu-id="5eef0-177">userid</span></span>              | <span data-ttu-id="5eef0-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="5eef0-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="5eef0-179">a.</span><span class="sxs-lookup"><span data-stu-id="5eef0-179">a.</span></span> <span data-ttu-id="5eef0-180">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5eef0-183">b.</span><span class="sxs-lookup"><span data-stu-id="5eef0-183">b.</span></span> <span data-ttu-id="5eef0-184">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="5eef0-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5eef0-185">c.</span><span class="sxs-lookup"><span data-stu-id="5eef0-185">c.</span></span> <span data-ttu-id="5eef0-186">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="5eef0-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5eef0-187">d.</span><span class="sxs-lookup"><span data-stu-id="5eef0-187">d.</span></span> <span data-ttu-id="5eef0-188">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5eef0-189">Antes de configurar la aserción SAML, debe ponerse en contacto con el [soporte técnico de ADP GlobalView](https://www.adp.com/contact-us/overview.aspx) y solicitar el valor del atributo de identificador único para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="5eef0-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="5eef0-190">Necesitará este valor para configurar la notificación personalizada para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="5eef0-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="5eef0-191">En la sección **Configuración de ADP Globalview**, haga clic en **Configurar ADP Globalview** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5eef0-192">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="5eef0-194">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5eef0-194">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="5eef0-196">Para configurar el inicio de sesión único en **ADP GlobalView**, es preciso enviar los valores descargados de **Certificado (Base64)**, **Sign-Out URL (Dirección URL de cierre de sesión), SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [soporte técnico de ADP GlobalView](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="5eef0-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="5eef0-197">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5eef0-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5eef0-198">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5eef0-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5eef0-199">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5eef0-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5eef0-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eef0-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="5eef0-201">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5eef0-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5eef0-203">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="5eef0-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5eef0-204">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="5eef0-206">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5eef0-208">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5eef0-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5eef0-210">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="5eef0-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5eef0-212">a.</span><span class="sxs-lookup"><span data-stu-id="5eef0-212">a.</span></span> <span data-ttu-id="5eef0-213">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5eef0-214">b.</span><span class="sxs-lookup"><span data-stu-id="5eef0-214">b.</span></span> <span data-ttu-id="5eef0-215">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5eef0-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5eef0-216">c.</span><span class="sxs-lookup"><span data-stu-id="5eef0-216">c.</span></span> <span data-ttu-id="5eef0-217">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5eef0-218">d.</span><span class="sxs-lookup"><span data-stu-id="5eef0-218">d.</span></span> <span data-ttu-id="5eef0-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="5eef0-220">Creación de un usuario de prueba de ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="5eef0-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="5eef0-221">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="5eef0-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="5eef0-222">Colabore con el [soporte técnico de ADP GlobalView](https://www.adp.com/contact-us/overview.aspx) para agregar usuarios a la cuenta de ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="5eef0-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5eef0-223">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eef0-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5eef0-224">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="5eef0-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5eef0-226">**Para asignar a Britta Simon a ADP GlobalView, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="5eef0-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="5eef0-227">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5eef0-229">En la lista de aplicaciones, seleccione **ADP GlobalView**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="5eef0-231">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5eef0-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-233">Click **Add** button.</span></span> <span data-ttu-id="5eef0-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5eef0-236">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="5eef0-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5eef0-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5eef0-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5eef0-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5eef0-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5eef0-239">Testing single sign-on</span></span>

<span data-ttu-id="5eef0-240">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5eef0-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="5eef0-241">Al hacer clic en el icono de ADP GlobalView en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="5eef0-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5eef0-242">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5eef0-242">Additional resources</span></span>

* [<span data-ttu-id="5eef0-243">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5eef0-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5eef0-244">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5eef0-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

