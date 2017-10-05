---
title: "Tutorial: Integración de Azure Active Directory con Absorb LMS | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Absorb LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="d4ec0-103">Tutorial: Integración de Azure Active Directory con Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="d4ec0-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="d4ec0-104">En este tutorial, aprenderá a integrar Absorb LMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d4ec0-105">La integración de Absorb LMS con Azure AD ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d4ec0-106">Puede controlar en Azure AD quién tiene acceso a Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="d4ec0-107">Puede permitir que los usuarios inicien sesión automáticamente en Absorb LMS (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d4ec0-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d4ec0-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="d4ec0-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d4ec0-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4ec0-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d4ec0-111">Prerequisites</span></span>

<span data-ttu-id="d4ec0-112">Para configurar la integración de Azure AD con Absorb LMS, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="d4ec0-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4ec0-113">An Azure AD subscription</span></span>
- <span data-ttu-id="d4ec0-114">Una suscripción habilitada para inicio de sesión único en Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="d4ec0-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d4ec0-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d4ec0-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d4ec0-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d4ec0-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d4ec0-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d4ec0-119">Scenario description</span></span>
<span data-ttu-id="d4ec0-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d4ec0-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d4ec0-122">Adición de Absorb LMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="d4ec0-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="d4ec0-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4ec0-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="d4ec0-124">Adición de Absorb LMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="d4ec0-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="d4ec0-125">Para configurar la integración de Absorb LMS en Azure AD, será preciso que agregue Absorb LMS desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d4ec0-126">**Para agregar Absorb LMS desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d4ec0-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ec0-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="d4ec0-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d4ec0-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-130">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="d4ec0-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="d4ec0-134">En el cuadro de búsqueda, escriba **Absorb LMS**, seleccione **Absorb LMS** en el panel de resultados y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![Absorb LMS en la lista de resultados](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d4ec0-136">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4ec0-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d4ec0-137">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Absorb LMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d4ec0-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d4ec0-138">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Absorb LMS para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="d4ec0-139">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="d4ec0-140">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor del **Username** (Nombre de usuario) en Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="d4ec0-141">Para configurar y probar el inicio de sesión único de Azure AD con Absorb LMS, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d4ec0-142">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d4ec0-143">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d4ec0-144">**[Creación de un usuario de prueba de Absorb LMS](#create-an-absorb-lms-test-user)**: para tener un homólogo de Britta Simon en Absorb LMS que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d4ec0-145">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d4ec0-146">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d4ec0-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4ec0-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d4ec0-148">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="d4ec0-149">**Para configurar el inicio de sesión único de Azure AD con Absorb LMS, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d4ec0-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ec0-150">En la página de integración de la aplicación **Absorb LMS** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="d4ec0-152">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="d4ec0-154">En la sección de **dominio y direcciones URL de Absorb LMS**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="d4ec0-156">a.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-156">a.</span></span> <span data-ttu-id="d4ec0-157">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="d4ec0-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="d4ec0-158">b.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-158">b.</span></span> <span data-ttu-id="d4ec0-159">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.myabsorb.com/Account/SAML`.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d4ec0-160">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-160">These values are not the real.</span></span> <span data-ttu-id="d4ec0-161">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d4ec0-162">Póngase en contacto con el [equipo de soporte técnico de Absorb LMS](https://www.absorblms.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="d4ec0-163">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="d4ec0-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d4ec0-165">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d4ec0-167">En la sección **Configuración de Absorb LMS**, haga clic en **Configurar Absorb LMS** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d4ec0-168">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="d4ec0-170">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="d4ec0-171">Haga clic en el **icono de cuenta** de la interfaz de administración.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="d4ec0-173">Haga clic en **Portal Settings** (Configuración del portal).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-173">Click **Portal Settings**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="d4ec0-175">Haga clic en la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="d4ec0-175">Click the **Users** tab.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="d4ec0-177">Siga estos pasos para acceder a los campos de configuración de inicio de sesión único:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="d4ec0-179">a.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-179">a.</span></span> <span data-ttu-id="d4ec0-180">Seleccione el **Mode** (Modo) adecuado.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="d4ec0-181">b.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-181">b.</span></span> <span data-ttu-id="d4ec0-182">Abra el certificado que ha descargado de Azure Portal en el Bloc de notas, quite las etiquetas **---BEGIN CERTIFICATE---** y **---END CERTIFICATE---** y pegue el resto del contenido en el cuadro de texto **Key** (Clave).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="d4ec0-183">c.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-183">c.</span></span> <span data-ttu-id="d4ec0-184">En el cuadro de texto **Id Property** (Propiedad Id), seleccione el atributo adecuado que ha configurado como identificador de usuario en Azure AD; por ejemplo, si se selecciona userprinciplename en Azure AD, aquí se seleccionaría Username (Nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="d4ec0-185">d.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-185">d.</span></span> <span data-ttu-id="d4ec0-186">En el cuadro de texto **Login URL** (URL de inicio de sesión), pegue el valor de **"URL del servicio de inicio de sesión único de SAML"** que copió de la ventana **Configurar inicio de sesión** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="d4ec0-187">e.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-187">e.</span></span> <span data-ttu-id="d4ec0-188">En el cuadro de texto **Logout URL** (URL de cierre de sesión), pegue el valor de **"Dirección URL de cierre de sesión"** que copió de la ventana **Configurar inicio de sesión** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="d4ec0-189">Habilite **"Only Allow SSO Login"** (Solo permitir inicio de sesión SSO).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="d4ec0-191">Haga clic en **"Save"** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="d4ec0-192">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d4ec0-193">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d4ec0-194">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d4ec0-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d4ec0-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4ec0-195">Create an Azure AD test user</span></span>

<span data-ttu-id="d4ec0-196">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d4ec0-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="d4ec0-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d4ec0-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ec0-199">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d4ec0-201">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d4ec0-203">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d4ec0-205">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d4ec0-207">a.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-207">a.</span></span> <span data-ttu-id="d4ec0-208">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d4ec0-209">b.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-209">b.</span></span> <span data-ttu-id="d4ec0-210">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d4ec0-211">c.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-211">c.</span></span> <span data-ttu-id="d4ec0-212">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d4ec0-213">d.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-213">d.</span></span> <span data-ttu-id="d4ec0-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="d4ec0-215">Creación de un usuario de prueba de Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="d4ec0-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="d4ec0-216">Para permitir que los usuarios de Azure AD inicien sesión en Absorb LMS, tienen que aprovisionarse en Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="d4ec0-217">En el caso de Absorb LMS, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="d4ec0-218">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d4ec0-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ec0-219">Inicie sesión como administrador en el sitio de la compañía de Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="d4ec0-220">Haga clic en la pestaña **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-220">Click **Users** tab.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="d4ec0-222">En la pestaña **Users** (Usuarios), haga clic en **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-222">Click **Users** under the **Users** tab.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="d4ec0-224">Seleccione **User** (Usuario) de la lista desplegable **Add New** (Agregar nuevo).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-224">Select **User** from **Add New** drop-down.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="d4ec0-226">En la página **Add User** (Agregar usuario), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d4ec0-226">On the **Add User** page, perform the following steps:</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="d4ec0-228">a.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-228">a.</span></span> <span data-ttu-id="d4ec0-229">En el cuadro de texto **First Name** (Nombre), escriba el nombre, por ejemplo, Britta.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="d4ec0-230">b.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-230">b.</span></span> <span data-ttu-id="d4ec0-231">En el cuadro de texto **Last Name** (Apellido), escriba el apellido, por ejemplo, Simon.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="d4ec0-232">c.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-232">c.</span></span> <span data-ttu-id="d4ec0-233">En el cuadro de texto **Username** (Nombre de usuario), escriba el nombre de usuario, por ejemplo, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="d4ec0-234">d.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-234">d.</span></span> <span data-ttu-id="d4ec0-235">En el cuadro de texto **Password** (Contraseña), escriba la contraseña de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="d4ec0-236">e.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-236">e.</span></span> <span data-ttu-id="d4ec0-237">En el cuadro de texto **Confirm Password** (Confirmar contraseña), escriba la misma contraseña.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="d4ec0-238">f.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-238">f.</span></span> <span data-ttu-id="d4ec0-239">Establézcalo en **ACTIVE** (ACTIVO).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="d4ec0-240">Haga clic en **"Save"** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d4ec0-241">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4ec0-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="d4ec0-242">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![Asignación del rol de usuario][200]

<span data-ttu-id="d4ec0-244">**Para asignar a Britta Simon a Absorb LMS, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d4ec0-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ec0-245">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d4ec0-247">En la lista de aplicaciones, seleccione **Absorb LMS**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-247">In the applications list, select **Absorb LMS**.</span></span>

    ![Vínculo a Absorb LMS en la lista de aplicaciones](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="d4ec0-249">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="d4ec0-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-251">Click **Add** button.</span></span> <span data-ttu-id="d4ec0-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="d4ec0-254">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d4ec0-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d4ec0-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d4ec0-257">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d4ec0-257">Test single sign-on</span></span>

<span data-ttu-id="d4ec0-258">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d4ec0-259">Al hacer clic en el icono de Absorb LMS del panel de acceso, debería iniciar sesión automáticamente en su aplicación Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="d4ec0-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="d4ec0-260">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d4ec0-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4ec0-261">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d4ec0-261">Additional resources</span></span>

* [<span data-ttu-id="d4ec0-262">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4ec0-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d4ec0-263">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d4ec0-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

