---
title: "Tutorial: Integración de Azure Active Directory con Druva | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="2a4d2-103">Tutorial: Integración de Azure Active Directory con Druva</span><span class="sxs-lookup"><span data-stu-id="2a4d2-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="2a4d2-104">En este tutorial, obtendrá información sobre cómo integrar Druva con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a4d2-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a4d2-105">La integración de Druva con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2a4d2-106">Puede controlar en Azure AD quién tiene acceso a Druva.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="2a4d2-107">Puede permitir que los usuarios inicien sesión automáticamente en Druva (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2a4d2-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2a4d2-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a4d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a4d2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a4d2-110">Prerequisites</span></span>

<span data-ttu-id="2a4d2-111">Para configurar la integración de Azure AD con Druva, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="2a4d2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a4d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a4d2-113">Una suscripción habilitada para el inicio de sesión único en Druva</span><span class="sxs-lookup"><span data-stu-id="2a4d2-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a4d2-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a4d2-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a4d2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2a4d2-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a4d2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a4d2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2a4d2-118">Scenario description</span></span>
<span data-ttu-id="2a4d2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a4d2-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a4d2-121">Incorporación de Druva desde la galería</span><span class="sxs-lookup"><span data-stu-id="2a4d2-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="2a4d2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a4d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="2a4d2-123">Incorporación de Druva desde la galería</span><span class="sxs-lookup"><span data-stu-id="2a4d2-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="2a4d2-124">Para configurar la integración de Druva en Azure AD, tendrá que agregar Druva desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2a4d2-125">**Para agregar Druva desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2a4d2-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2a4d2-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="2a4d2-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2a4d2-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="2a4d2-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="2a4d2-133">En el cuadro de búsqueda, escriba **Druva**, seleccione **Druva** en el panel de resultados y, luego, haga clic en el botón **Agregar** para añadir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva en la lista de resultados](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2a4d2-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a4d2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2a4d2-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Druva con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2a4d2-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a4d2-137">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Druva para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="2a4d2-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Druva.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="2a4d2-139">Para establecer la relación de vínculo, en Druva, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2a4d2-140">Para configurar y probar el inicio de sesión único de Azure AD con Druva, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2a4d2-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2a4d2-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a4d2-143">**[Creación de un usuario de prueba de Druva](#create-a-druva-test-user)**: para tener un homólogo de Britta Simon en Druva que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2a4d2-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a4d2-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2a4d2-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a4d2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2a4d2-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Druva.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="2a4d2-148">**Para configurar el inicio de sesión único de Azure AD con Druva, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2a4d2-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="2a4d2-149">En Azure Portal, en la página de integración de la aplicación **Druva**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="2a4d2-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="2a4d2-153">En la sección **Dominio y direcciones URL de Druva**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="2a4d2-155">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="2a4d2-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="2a4d2-156">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="2a4d2-158">La aplicación Druva espera las aserciones de SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los **atributos del token SAML**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="2a4d2-160">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo del token de SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="2a4d2-161">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="2a4d2-161">Attribute Name</span></span>      | <span data-ttu-id="2a4d2-162">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="2a4d2-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="2a4d2-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="2a4d2-163">insync\_auth\_token</span></span> |<span data-ttu-id="2a4d2-164">Escriba el valor del token generado</span><span class="sxs-lookup"><span data-stu-id="2a4d2-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="2a4d2-165">a.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-165">a.</span></span> <span data-ttu-id="2a4d2-166">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="2a4d2-169">b.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-169">b.</span></span> <span data-ttu-id="2a4d2-170">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="2a4d2-171">c.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-171">c.</span></span> <span data-ttu-id="2a4d2-172">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="2a4d2-173">El valor del token generado se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="2a4d2-174">d.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-174">d.</span></span> <span data-ttu-id="2a4d2-175">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="2a4d2-176">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2a4d2-176">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2a4d2-178">En la sección **Configuración de Druva**, haga clic en **Configurar Druva** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2a4d2-179">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="2a4d2-181">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía en Druva.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="2a4d2-182">Vaya a **Administrar \> Configuración**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="2a4d2-183">![Configuración](./media/active-directory-saas-druva-tutorial/ic795091.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="2a4d2-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="2a4d2-184">En el cuadro de diálogo Single Sign-On Settings (Configuración de inicio de sesión único), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="2a4d2-185">![Configuración de inicio de sesión único](./media/active-directory-saas-druva-tutorial/ic795092.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="2a4d2-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="2a4d2-186">a.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-186">a.</span></span> <span data-ttu-id="2a4d2-187">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que copió de Azure Portal en el cuadro de texto **ID Provider Login URL** (Dirección URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="2a4d2-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="2a4d2-188">b.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-188">b.</span></span> <span data-ttu-id="2a4d2-189">Pegue el valor de **Sign-Out URL** (Dirección URL de cierre de sesión) que copió de Azure Portal en el cuadro de texto **ID Provider Logout URL** (Dirección URL de cierre de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="2a4d2-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="2a4d2-190">c.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-190">c.</span></span> <span data-ttu-id="2a4d2-191">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de proveedor de Id.** .</span><span class="sxs-lookup"><span data-stu-id="2a4d2-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="2a4d2-192">d.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-192">d.</span></span> <span data-ttu-id="2a4d2-193">Para abrir la página **Configuración**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="2a4d2-194">En la página **Configuración**, haga clic en**Generar token de SSO**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="2a4d2-195">![Configuración](./media/active-directory-saas-druva-tutorial/ic795093.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="2a4d2-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="2a4d2-196">En el cuadro de diálogo **Token de autenticación de inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="2a4d2-197">![Token de SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token de SSO")</span><span class="sxs-lookup"><span data-stu-id="2a4d2-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="2a4d2-198">a.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-198">a.</span></span> <span data-ttu-id="2a4d2-199">Haga clic en **Copiar**, pegue el valor copiado en el cuadro de texto **Valor** en la sección **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="2a4d2-200">b.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-200">b.</span></span> <span data-ttu-id="2a4d2-201">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="2a4d2-202">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2a4d2-203">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2a4d2-204">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2a4d2-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2a4d2-205">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a4d2-205">Create an Azure AD test user</span></span>

<span data-ttu-id="2a4d2-206">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2a4d2-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="2a4d2-208">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2a4d2-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2a4d2-209">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2a4d2-211">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2a4d2-213">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2a4d2-215">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2a4d2-217">a.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-217">a.</span></span> <span data-ttu-id="2a4d2-218">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a4d2-219">b.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-219">b.</span></span> <span data-ttu-id="2a4d2-220">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2a4d2-221">c.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-221">c.</span></span> <span data-ttu-id="2a4d2-222">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2a4d2-223">d.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-223">d.</span></span> <span data-ttu-id="2a4d2-224">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="2a4d2-225">Crear un usuario de prueba de Druva</span><span class="sxs-lookup"><span data-stu-id="2a4d2-225">Create a Druva test user</span></span>

<span data-ttu-id="2a4d2-226">Para permitir que los usuarios de Azure AD inicien sesión en Druva, tiene que aprovisionarse en Druva.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="2a4d2-227">En el caso de Druva, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="2a4d2-228">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="2a4d2-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="2a4d2-229">Inicie sesión en el sitio de la compañía de **Druva** como administrador.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="2a4d2-230">Vaya a **Administrar \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="2a4d2-231">![Administración de usuarios](./media/active-directory-saas-druva-tutorial/ic795097.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="2a4d2-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="2a4d2-232">Haga clic en **Create New**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="2a4d2-233">![Administración de usuarios](./media/active-directory-saas-druva-tutorial/ic795098.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="2a4d2-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="2a4d2-234">En el cuadro de diálogo Create New User (Crear nuevo usuario), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2a4d2-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="2a4d2-235">![Creación de un nuevo usuario](./media/active-directory-saas-druva-tutorial/ic795099.png "Creación de un nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="2a4d2-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="2a4d2-236">a.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-236">a.</span></span> <span data-ttu-id="2a4d2-237">En el cuadro de texto **Email address** (Dirección de correo electrónico), escriba el correo electrónico del usuario, en este caso, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="2a4d2-238">b.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-238">b.</span></span> <span data-ttu-id="2a4d2-239">En el cuadro de texto **Name** (Nombre), escriba el nombre de usuario, por ejemplo, **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="2a4d2-240">c.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-240">c.</span></span> <span data-ttu-id="2a4d2-241">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="2a4d2-242">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Druva que proporcione Druva para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2a4d2-243">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a4d2-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="2a4d2-244">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Druva.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="2a4d2-246">**Para asignar el usuario Britta Simon a Druva, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2a4d2-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="2a4d2-247">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2a4d2-249">En la lista de aplicaciones, seleccione **Druva**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-249">In the applications list, select **Druva**.</span></span>

    ![Vínculo a Druva en la lista de aplicaciones](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="2a4d2-251">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="2a4d2-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-253">Click **Add** button.</span></span> <span data-ttu-id="2a4d2-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="2a4d2-256">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2a4d2-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a4d2-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2a4d2-259">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="2a4d2-259">Test single sign-on</span></span>

<span data-ttu-id="2a4d2-260">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2a4d2-261">Al hacer clic en el icono de Druva en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Druva.</span><span class="sxs-lookup"><span data-stu-id="2a4d2-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="2a4d2-262">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2a4d2-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2a4d2-263">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2a4d2-263">Additional resources</span></span>

* [<span data-ttu-id="2a4d2-264">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a4d2-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a4d2-265">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2a4d2-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

