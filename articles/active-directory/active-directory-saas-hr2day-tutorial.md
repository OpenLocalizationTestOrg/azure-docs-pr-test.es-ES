---
title: "Tutorial: integración de Azure Active Directory con HR2day by Merces | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y HR2day by Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 77e2fcf9c306259286b15767f3a992510d6d79d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="424e5-103">Tutorial: Integración de Azure Active Directory con HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="424e5-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="424e5-104">En este tutorial, obtendrá información sobre cómo integrar HR2day by Merces con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="424e5-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="424e5-105">La integración de HR2day by Merces con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="424e5-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="424e5-106">Puede controlar en Azure AD quién tiene acceso a HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="424e5-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="424e5-107">Puede permitir que los usuarios inicien sesión automáticamente en HR2day by Merces con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="424e5-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="424e5-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="424e5-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="424e5-109">Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="424e5-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="424e5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="424e5-110">Prerequisites</span></span>

<span data-ttu-id="424e5-111">Para configurar la integración de Azure AD con HR2day by Merces, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="424e5-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="424e5-112">Una suscripción de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="424e5-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="424e5-113">Una suscripción habilitada para el inicio de sesión único en HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="424e5-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="424e5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="424e5-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="424e5-115">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="424e5-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="424e5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="424e5-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="424e5-117">Puede obtener [un versión de evaluación gratuita de un mes de Azure AD](https://azure.microsoft.com/pricing/free-trial/) si aún no la tiene.</span><span class="sxs-lookup"><span data-stu-id="424e5-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="424e5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="424e5-118">Scenario description</span></span>
<span data-ttu-id="424e5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="424e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="424e5-120">La escenario descrito aquí consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="424e5-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="424e5-121">Agregación de HR2day by Merces desde la galería.</span><span class="sxs-lookup"><span data-stu-id="424e5-121">Adding HR2day by Merces from the gallery.</span></span>
2. <span data-ttu-id="424e5-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="424e5-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="424e5-123">Agregación de HR2day by Merces desde la galería</span><span class="sxs-lookup"><span data-stu-id="424e5-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="424e5-124">Para configurar la integración de HR2day by Merces en Azure AD, debe agregar HR2day by Merces desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="424e5-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="424e5-125">**Para agregar HR2day by Merces desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="424e5-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="424e5-126">En el panel de navegación izquierdo de [Azure Portal](https://portal.azure.com), seleccione el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="424e5-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="424e5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="424e5-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="424e5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="424e5-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="424e5-131">Para agregar una nueva aplicación, seleccione el botón **Nueva aplicación** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="424e5-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="424e5-133">En el cuadro Buscar, escriba **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="424e5-133">In the search box, type **HR2day by Merces**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="424e5-135">En el panel de resultados, seleccione **HR2day by Merces** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="424e5-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="424e5-137">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="424e5-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="424e5-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con HR2day by Merces con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="424e5-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="424e5-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de HR2day by Merces para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="424e5-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="424e5-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="424e5-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="424e5-141">Para establecer la relación de vínculo, en HR2day by Merces, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="424e5-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="424e5-142">Para configurar y probar el inicio de sesión único de Azure AD con HR2day by Merces, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="424e5-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="424e5-143">[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on): permita que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="424e5-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
2. <span data-ttu-id="424e5-144">[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user): pruebe el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="424e5-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="424e5-145">[Creación de un usuario de prueba de HR2day by Merces](#creating-an-hr2day-by-merces-test-user): cree un homólogo de Britta Simon en HR2day by Merces que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="424e5-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="424e5-146">[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user): permita que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="424e5-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="424e5-147">[Prueba del inicio de sesión único](#testing-single-sign-on): compruebe que la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="424e5-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="424e5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="424e5-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="424e5-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="424e5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="424e5-150">**Para configurar el inicio de sesión único de Azure AD con HR2day by Merces, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="424e5-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="424e5-151">En Azure Portal, en la página de integración de la aplicación **HR2day by Merces**, seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="424e5-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="424e5-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="424e5-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="424e5-155">En la sección **Dominio y direcciones URL de HR2day by Merces**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="424e5-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="424e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="424e5-157">a.</span></span> <span data-ttu-id="424e5-158">En el cuadro de texto **Dirección URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="424e5-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="424e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="424e5-159">b.</span></span> <span data-ttu-id="424e5-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="424e5-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="424e5-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="424e5-161">These values are not real.</span></span> <span data-ttu-id="424e5-162">Debe actualizarlos con la dirección URL de inicio de sesión y el identificador reales.</span><span class="sxs-lookup"><span data-stu-id="424e5-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="424e5-163">Póngase en contacto con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="424e5-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


4. <span data-ttu-id="424e5-164">En la sección **Certificado de firma de SAML**, seleccione **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="424e5-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="424e5-166">Esta sección describe cómo se habilita la autenticación de usuarios en HR2day by Merces con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="424e5-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="424e5-167">Se realiza utilizando la federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="424e5-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="424e5-168">La aplicación HR2day by Merces espera las aserciones SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados al token SAML.</span><span class="sxs-lookup"><span data-stu-id="424e5-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="424e5-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="424e5-169">The following screenshot shows an example of this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="424e5-171">Antes de configurar la aserción SAML, debe ponerse en contacto con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl) y solicitar el valor del atributo de identificador único del inquilino.</span><span class="sxs-lookup"><span data-stu-id="424e5-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="424e5-172">Necesita este valor para completar los pasos descritos en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="424e5-172">You need this value to complete the steps in the next section.</span></span> 

6. <span data-ttu-id="424e5-173">En el cuadro de diálogo **Inicio de sesión único**, en la sección **Atributos de usuario**, configure el atributo token SAML como muestra la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="424e5-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="424e5-174">A continuación, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="424e5-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="424e5-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="424e5-175">Attribute name</span></span>    |   <span data-ttu-id="424e5-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="424e5-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="424e5-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="424e5-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="424e5-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="424e5-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="424e5-179">a.</span><span class="sxs-lookup"><span data-stu-id="424e5-179">a.</span></span> <span data-ttu-id="424e5-180">Seleccione **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="424e5-180">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="424e5-183">b.</span><span class="sxs-lookup"><span data-stu-id="424e5-183">b.</span></span> <span data-ttu-id="424e5-184">En el cuadro de texto **Nombre**, escriba **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="424e5-184">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="424e5-185">c.</span><span class="sxs-lookup"><span data-stu-id="424e5-185">c.</span></span> <span data-ttu-id="424e5-186">En la lista **Valor**, seleccione **Join()**.</span><span class="sxs-lookup"><span data-stu-id="424e5-186">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="424e5-187">d.</span><span class="sxs-lookup"><span data-stu-id="424e5-187">d.</span></span> <span data-ttu-id="424e5-188">En la lista **Cadena1**, seleccione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="424e5-188">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="424e5-189">e.</span><span class="sxs-lookup"><span data-stu-id="424e5-189">e.</span></span> <span data-ttu-id="424e5-190">Para **Cadena2**, escriba el identificador único proporcionado por el equipo de HR2day.</span><span class="sxs-lookup"><span data-stu-id="424e5-190">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="424e5-191">f.</span><span class="sxs-lookup"><span data-stu-id="424e5-191">f.</span></span> <span data-ttu-id="424e5-192">En el cuadro de texto **Separador**, escriba **@**.</span><span class="sxs-lookup"><span data-stu-id="424e5-192">In the **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="424e5-193">g.</span><span class="sxs-lookup"><span data-stu-id="424e5-193">g.</span></span> <span data-ttu-id="424e5-194">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="424e5-194">Select **Ok**.</span></span>

7. <span data-ttu-id="424e5-195">Seleccione el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="424e5-195">Select the **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="424e5-197">En la sección **Configuración de HR2day by Merces**, seleccione **Configurar HR2day by Merces** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="424e5-197">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="424e5-198">Copie la **Dirección URL de cierre de sesión**, el **Identificador de entidad de SAML** y la **Dirección URL del servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="424e5-198">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="424e5-200">Para configurar el SSO para la aplicación, póngase en contacto con el [equipo de soporte técnico de HR2day by Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="424e5-200">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="424e5-201">Adjunte el archivo de **Certificado (Base64)** descargado a su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="424e5-201">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="424e5-202">Además, proporcione la **dirección URL de cierre de sesión**, el **identificador de entidad de SAML** y la **dirección URL del servicio de inicio de sesión único de SAML** para que puedan configurar la integración del inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="424e5-202">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="424e5-203">Indique al equipo de Merces que esta integración necesita que el id. de entidad se establezca con el patrón **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="424e5-203">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="424e5-204">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="424e5-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="424e5-205">Después de agregar esta aplicación desde la sección **Active Directory** > **Aplicaciones empresariales**, seleccione la pestaña **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="424e5-205">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab.</span></span> <span data-ttu-id="424e5-206">A continuación, consulte la documentación insertada en la sección **Configuración** en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="424e5-206">Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="424e5-207">Puede leer más sobre la característica de documentación insertada en el artículo sobre la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="424e5-207">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="424e5-208">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="424e5-208">Create an Azure AD test user</span></span>
<span data-ttu-id="424e5-209">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="424e5-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="424e5-211">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="424e5-211">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="424e5-212">En el panel de navegación izquierdo de **Azure Portal**, seleccione el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="424e5-212">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="424e5-214">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, seleccione **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="424e5-214">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="424e5-216">En la parte superior del cuadro de diálogo, seleccione **Agregar** para abrir el cuadro de diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="424e5-216">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="424e5-218">En el cuadro de diálogo **Usuario**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="424e5-218">In the **User** dialog box, take the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="424e5-220">a.</span><span class="sxs-lookup"><span data-stu-id="424e5-220">a.</span></span> <span data-ttu-id="424e5-221">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="424e5-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="424e5-222">b.</span><span class="sxs-lookup"><span data-stu-id="424e5-222">b.</span></span> <span data-ttu-id="424e5-223">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="424e5-223">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="424e5-224">c.</span><span class="sxs-lookup"><span data-stu-id="424e5-224">c.</span></span> <span data-ttu-id="424e5-225">Seleccione **Mostrar contraseña** y anote la contraseña.</span><span class="sxs-lookup"><span data-stu-id="424e5-225">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="424e5-226">d.</span><span class="sxs-lookup"><span data-stu-id="424e5-226">d.</span></span> <span data-ttu-id="424e5-227">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="424e5-227">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="424e5-228">Creación de un usuario de prueba de HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="424e5-228">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="424e5-229">El objetivo de esta sección es crear una usuaria de prueba llamado Britta Simon en HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="424e5-229">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="424e5-230">Trabaje con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl) para agregar los usuarios en la cuenta de HR2day.</span><span class="sxs-lookup"><span data-stu-id="424e5-230">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="424e5-231">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="424e5-231">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="424e5-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="424e5-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="424e5-233">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="424e5-233">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="424e5-235">**Para asignar a Britta Simon a HR2day by Merces, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="424e5-235">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="424e5-236">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="424e5-236">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="424e5-237">A continuación, seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="424e5-237">Next, select **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="424e5-239">En la lista de aplicaciones, seleccione **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="424e5-239">In the applications list, select **HR2day by Merces**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="424e5-241">En el menú de la izquierda, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="424e5-241">In the menu on the left, select **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="424e5-243">Seleccione el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="424e5-243">Select the **Add** button.</span></span> <span data-ttu-id="424e5-244">Después, en el cuadro de diálogo **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="424e5-244">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="424e5-246">En el cuadro de diálogo **Usuarios y grupos**, en la lista **Usuarios** seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="424e5-246">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="424e5-247">Haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="424e5-247">Click the **Select** button.</span></span>

7. <span data-ttu-id="424e5-248">En el cuadro de diálogo **Agregar asignación**, seleccione **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="424e5-248">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="424e5-249">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="424e5-249">Test single sign-on</span></span>

<span data-ttu-id="424e5-250">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="424e5-250">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="424e5-251">Al seleccionar el icono de HR2day by Merces en el panel de acceso, iniciará sesión automáticamente en la aplicación HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="424e5-251">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="424e5-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="424e5-252">Additional resources</span></span>

* [<span data-ttu-id="424e5-253">Lista de tutoriales sobre la integración de aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="424e5-253">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="424e5-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="424e5-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

