---
title: "Tutorial: Integración de Azure Active Directory con Evidence.com | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="4044a-103">Tutorial: Integración de Azure Active Directory con Evidence.com</span><span class="sxs-lookup"><span data-stu-id="4044a-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="4044a-104">En este tutorial, obtendrá información sobre cómo integrar Evidence.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4044a-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4044a-105">La integración de Evidence.com con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4044a-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4044a-106">Puede controlar en Azure AD quién tiene acceso a Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="4044a-107">Puede habilitar a los usuarios para que inicien sesión automáticamente en Evidence.com (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4044a-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4044a-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4044a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4044a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4044a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4044a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4044a-110">Prerequisites</span></span>

<span data-ttu-id="4044a-111">Para configurar la integración de Azure AD con Evidence.com, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4044a-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="4044a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4044a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4044a-113">Una suscripción habilitada para el inicio de sesión único en Evidence.com</span><span class="sxs-lookup"><span data-stu-id="4044a-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4044a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4044a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4044a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4044a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4044a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4044a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4044a-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4044a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4044a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4044a-118">Scenario description</span></span>
<span data-ttu-id="4044a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4044a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4044a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="4044a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4044a-121">Incorporación de Evidence.com desde la Galería</span><span class="sxs-lookup"><span data-stu-id="4044a-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="4044a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4044a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="4044a-123">Incorporación de Evidence.com desde la Galería</span><span class="sxs-lookup"><span data-stu-id="4044a-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="4044a-124">Para configurar la integración de Evidence.com en Azure AD, será preciso que agregue Evidence.com desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="4044a-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4044a-125">**Para agregar Evidence.com desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4044a-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4044a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4044a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="4044a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4044a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4044a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4044a-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="4044a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4044a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="4044a-133">En el cuadro de búsqueda, escriba **Evidence.com**, seleccione **Evidence.com** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4044a-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![Evidence.com en la lista de resultados](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4044a-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="4044a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4044a-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Evidence.com con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4044a-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4044a-137">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Evidence.com para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4044a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="4044a-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="4044a-139">Para establecer la relación de vínculo, en Evidence.com, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4044a-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4044a-140">Para configurar y probar el inicio de sesión único de Azure AD con Evidence.com, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4044a-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4044a-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="4044a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4044a-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4044a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4044a-143">**[Creación de un usuario de prueba de Evidence.com](#create-a-evidencecom-test-user)**: para tener un homólogo de Britta Simon en Evidence.com que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4044a-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4044a-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4044a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4044a-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="4044a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4044a-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4044a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4044a-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="4044a-148">**Para configurar el inicio de sesión único de Azure AD con Evidence.com, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4044a-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="4044a-149">En Azure Portal, en la página de integración de la aplicación **Evidence.com**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4044a-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="4044a-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4044a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="4044a-153">En la sección **Dominio y direcciones URL de Evidence.com**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4044a-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="4044a-155">a.</span><span class="sxs-lookup"><span data-stu-id="4044a-155">a.</span></span> <span data-ttu-id="4044a-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<yourtenant>.evidence.com`.</span><span class="sxs-lookup"><span data-stu-id="4044a-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="4044a-157">b.</span><span class="sxs-lookup"><span data-stu-id="4044a-157">b.</span></span> <span data-ttu-id="4044a-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="4044a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4044a-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4044a-159">These values are not real.</span></span> <span data-ttu-id="4044a-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4044a-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4044a-161">Póngase en contacto con el [equipo de soporte técnico al cliente de Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="4044a-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="4044a-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4044a-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="4044a-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4044a-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4044a-166">En la sección **Configuración de Evidence.com**, haga clic en **Configurar Evidence.com** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="4044a-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4044a-167">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="4044a-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="4044a-169">En una ventana de explorador web diferente, inicie sesión como administrador en su inquilino de Evidence.com y vaya a la pestaña **Admin** (Administrador).</span><span class="sxs-lookup"><span data-stu-id="4044a-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="4044a-170">Haga clic en **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="4044a-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="4044a-171">Seleccione **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="4044a-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="4044a-172">Copie los valores **SAML Entity ID** (Identificador de entidad de SAML), **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) y **Sign-Out URL** (Dirección URL de cierre de sesión) que se muestran en Azure Portal en los campos correspondientes en Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="4044a-173">Abra el archivo descargado de certificado (Base64) en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="4044a-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="4044a-174">Guarde la configuración en Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="4044a-175">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4044a-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4044a-176">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4044a-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4044a-177">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4044a-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4044a-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4044a-178">Create an Azure AD test user</span></span>

<span data-ttu-id="4044a-179">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4044a-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="4044a-181">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="4044a-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4044a-182">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4044a-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4044a-184">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4044a-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4044a-186">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4044a-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4044a-188">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4044a-188">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4044a-190">a.</span><span class="sxs-lookup"><span data-stu-id="4044a-190">a.</span></span> <span data-ttu-id="4044a-191">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4044a-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4044a-192">b.</span><span class="sxs-lookup"><span data-stu-id="4044a-192">b.</span></span> <span data-ttu-id="4044a-193">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4044a-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4044a-194">c.</span><span class="sxs-lookup"><span data-stu-id="4044a-194">c.</span></span> <span data-ttu-id="4044a-195">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4044a-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4044a-196">d.</span><span class="sxs-lookup"><span data-stu-id="4044a-196">d.</span></span> <span data-ttu-id="4044a-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4044a-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="4044a-198">Creación de un usuario de prueba de Evidence.com</span><span class="sxs-lookup"><span data-stu-id="4044a-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="4044a-199">Para que los usuarios de Azure AD puedan iniciar sesión, se les debe aprovisionar para el acceso dentro de la aplicación Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="4044a-200">En esta sección, se describe cómo crear cuentas de usuario de Azure AD en Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="4044a-201">**Para aprovisionar una cuenta de usuario en Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="4044a-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="4044a-202">En una ventana del explorador web, inicie sesión en el sitio de la compañía en Evidence.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="4044a-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="4044a-203">Vaya a pestaña **Admin** (Administrador).</span><span class="sxs-lookup"><span data-stu-id="4044a-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="4044a-204">Haga clic en **Add User**(Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="4044a-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="4044a-205">Haga clic en el botón **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="4044a-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="4044a-206">El valor de **Email Address** (Dirección de correo electrónico) del usuario agregado debe coincidir con el nombre de usuario en Azure AD de los usuarios a quienes desea conceder acceso.</span><span class="sxs-lookup"><span data-stu-id="4044a-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="4044a-207">Si el nombre de usuario y la dirección de correo electrónico no usan el mismo valor en su organización, puede usar la sección **Evidence.com > Atributos > Inicio de sesión único** de Azure Portal para hacer que el identificador de nombre enviado a Evidence.com sea la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="4044a-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4044a-208">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4044a-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="4044a-209">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="4044a-211">**Para asignar a Britta Simon a Evidence.com, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4044a-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="4044a-212">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4044a-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4044a-214">En la lista de aplicaciones, seleccione **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="4044a-214">In the applications list, select **Evidence.com**.</span></span>

    ![Vínculo a Evidence.com en la lista de aplicaciones](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="4044a-216">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4044a-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="4044a-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4044a-218">Click **Add** button.</span></span> <span data-ttu-id="4044a-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4044a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="4044a-221">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4044a-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4044a-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4044a-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4044a-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4044a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4044a-224">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="4044a-224">Test single sign-on</span></span>

<span data-ttu-id="4044a-225">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4044a-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4044a-226">Al hacer clic en el icono de Evidence.com en el panel de acceso, debe iniciar sesión automáticamente en su aplicación de Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4044a-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="4044a-227">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4044a-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4044a-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4044a-228">Additional resources</span></span>

* [<span data-ttu-id="4044a-229">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4044a-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4044a-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4044a-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

