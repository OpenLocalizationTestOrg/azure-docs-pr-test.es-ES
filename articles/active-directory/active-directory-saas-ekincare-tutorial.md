---
title: "Tutorial: integración de Azure Active Directory con eKincare | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="d2661-103">Tutorial: integración de Azure Active Directory con eKincare</span><span class="sxs-lookup"><span data-stu-id="d2661-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="d2661-104">En este tutorial, aprenderá a integrar eKincare con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2661-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2661-105">La integración de eKincare con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d2661-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d2661-106">Puede controlar en Azure AD quién tiene acceso a eKincare</span><span class="sxs-lookup"><span data-stu-id="d2661-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="d2661-107">Puede habilitar que los usuarios inicien sesión automáticamente en eKincare (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2661-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2661-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d2661-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d2661-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2661-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2661-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d2661-110">Prerequisites</span></span>

<span data-ttu-id="d2661-111">Para configurar la integración de Azure AD con eKincare, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d2661-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="d2661-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2661-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2661-113">Una suscripción habilitada para el inicio de sesión único en eKincare</span><span class="sxs-lookup"><span data-stu-id="d2661-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d2661-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d2661-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d2661-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d2661-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2661-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d2661-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d2661-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2661-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2661-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d2661-118">Scenario description</span></span>
<span data-ttu-id="d2661-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d2661-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2661-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d2661-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2661-121">Incorporación de eKincare desde la galería</span><span class="sxs-lookup"><span data-stu-id="d2661-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="d2661-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2661-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="d2661-123">Incorporación de eKincare desde la galería</span><span class="sxs-lookup"><span data-stu-id="d2661-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="d2661-124">Para configurar la integración de eKincare en Azure AD, es preciso agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d2661-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d2661-125">**Para agregar eKincare desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d2661-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d2661-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2661-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d2661-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d2661-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d2661-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d2661-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d2661-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d2661-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d2661-133">En el cuadro de búsqueda, escriba **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="d2661-133">In the search box, type **eKincare**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="d2661-135">En el panel de resultados, seleccione **eKincare** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2661-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d2661-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2661-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d2661-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con eKincare con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2661-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d2661-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de eKincare para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2661-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="d2661-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de eKincare.</span><span class="sxs-lookup"><span data-stu-id="d2661-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="d2661-141">Para establecer la relación de vínculo, en eKincare, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d2661-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d2661-142">Para configurar y probar el inicio de sesión único de Azure AD con eKincare, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d2661-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d2661-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d2661-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d2661-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2661-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2661-145">**[Creación de un usuario de prueba de eKincare](#creating-a-ekincare-test-user)**: para tener un homólogo de Britta Simon en eKincare vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2661-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d2661-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2661-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2661-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d2661-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d2661-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2661-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d2661-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación eKincare.</span><span class="sxs-lookup"><span data-stu-id="d2661-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="d2661-150">**Para configurar el inicio de sesión único de Azure AD con eKincare, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d2661-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="d2661-151">En Azure Portal, en la página de integración de la aplicación **eKincare**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d2661-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d2661-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d2661-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="d2661-155">En la sección **eKincare Domain and URLs** (Dominio y direcciones URL de eKincare), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d2661-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="d2661-157">a.</span><span class="sxs-lookup"><span data-stu-id="d2661-157">a.</span></span> <span data-ttu-id="d2661-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="d2661-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="d2661-159">b.</span><span class="sxs-lookup"><span data-stu-id="d2661-159">b.</span></span> <span data-ttu-id="d2661-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.ekincare.com/hul/saml`.</span><span class="sxs-lookup"><span data-stu-id="d2661-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d2661-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="d2661-161">These values are not real.</span></span> <span data-ttu-id="d2661-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="d2661-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d2661-163">Póngase en contacto con el [equipo de soporte técnico de eKincare](mailto:tech@ekincare.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="d2661-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="d2661-164">La aplicación eKincare espera las instrucciones de aserción de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="d2661-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d2661-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2661-165">Configure the following claims for this application.</span></span> <span data-ttu-id="d2661-166">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d2661-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="d2661-167">En la siguiente captura de pantalla se muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="d2661-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="d2661-168">El nombre de la notificación siempre será **"employeeid"**, cuyo valor hemos asignado a extensionattribute1, que contiene el valor de employeeid del usuario.</span><span class="sxs-lookup"><span data-stu-id="d2661-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="d2661-169">Los otros dos nombres de notificación, es decir,</span><span class="sxs-lookup"><span data-stu-id="d2661-169">The other two claims' name i.e</span></span> <span data-ttu-id="d2661-170">**"organizationid"** y **"organizationname"**, siempre serán los mismos y sus valores contendrán los detalles de la organización del usuario.</span><span class="sxs-lookup"><span data-stu-id="d2661-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="d2661-172">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d2661-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="d2661-173">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="d2661-173">Attribute Name</span></span> | <span data-ttu-id="d2661-174">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="d2661-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="d2661-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="d2661-175">employeeid</span></span> | <span data-ttu-id="d2661-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="d2661-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="d2661-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="d2661-177">organizationid</span></span> | <span data-ttu-id="d2661-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="d2661-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="d2661-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="d2661-179">organizationname</span></span> | <span data-ttu-id="d2661-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="d2661-180">*user.companyname*</span></span> |

    <span data-ttu-id="d2661-181">a.</span><span class="sxs-lookup"><span data-stu-id="d2661-181">a.</span></span> <span data-ttu-id="d2661-182">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="d2661-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="d2661-185">b.</span><span class="sxs-lookup"><span data-stu-id="d2661-185">b.</span></span> <span data-ttu-id="d2661-186">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="d2661-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d2661-187">c.</span><span class="sxs-lookup"><span data-stu-id="d2661-187">c.</span></span> <span data-ttu-id="d2661-188">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="d2661-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d2661-189">d.</span><span class="sxs-lookup"><span data-stu-id="d2661-189">d.</span></span> <span data-ttu-id="d2661-190">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d2661-190">Click **Ok**</span></span>

6. <span data-ttu-id="d2661-191">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d2661-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="d2661-193">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d2661-193">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d2661-195">Para configurar el inicio de sesión único en el lado de **eKincare**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="d2661-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="d2661-196">Ellos lo configuran para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="d2661-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d2661-197">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2661-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d2661-198">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d2661-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d2661-199">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d2661-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d2661-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2661-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="d2661-201">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d2661-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d2661-203">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d2661-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d2661-204">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2661-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2661-206">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d2661-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2661-208">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d2661-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2661-210">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d2661-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2661-212">a.</span><span class="sxs-lookup"><span data-stu-id="d2661-212">a.</span></span> <span data-ttu-id="d2661-213">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2661-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2661-214">b.</span><span class="sxs-lookup"><span data-stu-id="d2661-214">b.</span></span> <span data-ttu-id="d2661-215">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2661-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2661-216">c.</span><span class="sxs-lookup"><span data-stu-id="d2661-216">c.</span></span> <span data-ttu-id="d2661-217">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d2661-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d2661-218">d.</span><span class="sxs-lookup"><span data-stu-id="d2661-218">d.</span></span> <span data-ttu-id="d2661-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d2661-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="d2661-220">Creación de un usuario de prueba de eKincare</span><span class="sxs-lookup"><span data-stu-id="d2661-220">Creating a eKincare test user</span></span>

<span data-ttu-id="d2661-221">La aplicación admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crean automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2661-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d2661-222">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2661-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d2661-223">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a eKincare.</span><span class="sxs-lookup"><span data-stu-id="d2661-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d2661-225">**Para asignar a Britta Simon a eKincare, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d2661-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="d2661-226">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d2661-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d2661-228">En la lista de aplicaciones, seleccione **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="d2661-228">In the applications list, select **eKincare**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="d2661-230">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d2661-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d2661-232">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d2661-232">Click **Add** button.</span></span> <span data-ttu-id="d2661-233">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d2661-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d2661-235">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d2661-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d2661-236">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d2661-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2661-237">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d2661-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d2661-238">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d2661-238">Testing single sign-on</span></span>

<span data-ttu-id="d2661-239">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d2661-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d2661-240">Al hacer clic en el icono de eKincare en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación eKincare.</span><span class="sxs-lookup"><span data-stu-id="d2661-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="d2661-241">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2661-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2661-242">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d2661-242">Additional resources</span></span>

* [<span data-ttu-id="d2661-243">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2661-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2661-244">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d2661-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

