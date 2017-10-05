---
title: "Tutorial: Integración de Azure Active Directory con Front | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Front."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="6072f-103">Tutorial: integración de Azure Active Directory con Front</span><span class="sxs-lookup"><span data-stu-id="6072f-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="6072f-104">En este tutorial, obtendrá información sobre cómo integrar Front con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6072f-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6072f-105">Integrar Front con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6072f-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6072f-106">Puede controlar en Azure AD quién tiene acceso a Front.</span><span class="sxs-lookup"><span data-stu-id="6072f-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="6072f-107">Puede permitir que los usuarios inicien sesión automáticamente en Front (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6072f-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6072f-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6072f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6072f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6072f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6072f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6072f-110">Prerequisites</span></span>

<span data-ttu-id="6072f-111">Para configurar la integración de Azure AD con Front, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6072f-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="6072f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6072f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6072f-113">Una suscripción habilitada para el inicio de sesión único en Front</span><span class="sxs-lookup"><span data-stu-id="6072f-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6072f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6072f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6072f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6072f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6072f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6072f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6072f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6072f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6072f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6072f-118">Scenario description</span></span>
<span data-ttu-id="6072f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6072f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6072f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="6072f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6072f-121">Adición de Front desde la galería</span><span class="sxs-lookup"><span data-stu-id="6072f-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="6072f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6072f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="6072f-123">Adición de Front desde la galería</span><span class="sxs-lookup"><span data-stu-id="6072f-123">Adding Front from the gallery</span></span>
<span data-ttu-id="6072f-124">Para configurar la integración de Front en Azure AD, deberá agregar Front desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="6072f-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6072f-125">**Para agregar Front desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="6072f-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6072f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6072f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="6072f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6072f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6072f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6072f-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="6072f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6072f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="6072f-133">En el cuadro de búsqueda, escriba **Front**, seleccione **Front** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6072f-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Front en la lista de resultados](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6072f-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6072f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6072f-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Front con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6072f-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6072f-137">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Front para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6072f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="6072f-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Front.</span><span class="sxs-lookup"><span data-stu-id="6072f-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="6072f-139">Para establecer la relación de vínculo, en Front, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="6072f-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6072f-140">Para configurar y probar el inicio de sesión único de Azure AD con Front, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6072f-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6072f-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="6072f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6072f-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6072f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6072f-143">**[Creación de usuario de prueba de Front](#create-a-front-test-user)**: para tener un homólogo de Britta Simon en Front que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6072f-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6072f-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6072f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6072f-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="6072f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6072f-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6072f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6072f-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Front.</span><span class="sxs-lookup"><span data-stu-id="6072f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="6072f-148">**Para configurar el inicio de sesión único de Azure AD con Front, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6072f-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="6072f-149">En Azure Portal, en la página de integración de la aplicación **Front**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6072f-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="6072f-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6072f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="6072f-153">En la sección **Dominio y direcciones URL de Front**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="6072f-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="6072f-155">a.</span><span class="sxs-lookup"><span data-stu-id="6072f-155">a.</span></span> <span data-ttu-id="6072f-156">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="6072f-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="6072f-157">b.</span><span class="sxs-lookup"><span data-stu-id="6072f-157">b.</span></span> <span data-ttu-id="6072f-158">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.frontapp.com/sso/saml/callback`.</span><span class="sxs-lookup"><span data-stu-id="6072f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="6072f-159">Active **Mostrar configuración avanzada de URL**, si quiere configurar la aplicación en modo iniciado por **SP**.</span><span class="sxs-lookup"><span data-stu-id="6072f-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="6072f-161">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.frontapp.com`.</span><span class="sxs-lookup"><span data-stu-id="6072f-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="6072f-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="6072f-162">These values are not real.</span></span> <span data-ttu-id="6072f-163">Actualice estos valores con el identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión reales que se explican más adelante en el tutorial, o póngase en contacto con el [equipo de soporte técnico al cliente de Front](mailto:support@frontapp.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="6072f-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="6072f-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6072f-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="6072f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6072f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="6072f-168">En la sección **Configuración de Front**, haga clic en **Configurar Front** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="6072f-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6072f-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="6072f-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="6072f-171">Inicie la sesión en el inquilino de Front como administrador.</span><span class="sxs-lookup"><span data-stu-id="6072f-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="6072f-172">Vaya a **Settings (cog icon at the bottom of the left sidebar) > Preferences** (Configuración (icono de engranaje en la parte inferior de la barra lateral izquierda) > Preferencias).</span><span class="sxs-lookup"><span data-stu-id="6072f-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="6072f-174">Haga clic en el vínculo **Inicio de sesión único** .</span><span class="sxs-lookup"><span data-stu-id="6072f-174">Click **Single Sign On** link.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="6072f-176">Seleccione **SAML** en la lista desplegable de **Single Sign On** (Inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="6072f-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="6072f-178">En el cuadro de texto **Entry Point** (Punto de entrada), coloque el valor de **Dirección URL del servicio de inicio de sesión único** del Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6072f-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="6072f-180">Abra el archivo descargado de **certificado (Base64)** en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de firma**.</span><span class="sxs-lookup"><span data-stu-id="6072f-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="6072f-182">En la sección **Service provider settings** (configuración del proveedor de servicios), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6072f-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="6072f-184">a.</span><span class="sxs-lookup"><span data-stu-id="6072f-184">a.</span></span> <span data-ttu-id="6072f-185">Copie el valor de **Entity ID** (Identificador de entidad) y péguelo en el cuadro de texto **Identificador**, que se encuentra en la sección **Dominio y direcciones URL de Front** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6072f-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="6072f-186">b.</span><span class="sxs-lookup"><span data-stu-id="6072f-186">b.</span></span> <span data-ttu-id="6072f-187">Copie el valor de **ACS URL** y péguelo en el cuadro de texto **URL de inicio de sesión**, que se encuentra en la sección **Dominio y direcciones URL de Front** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6072f-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="6072f-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6072f-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="6072f-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6072f-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6072f-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6072f-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6072f-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6072f-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6072f-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6072f-192">Create an Azure AD test user</span></span>

<span data-ttu-id="6072f-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6072f-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="6072f-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="6072f-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6072f-196">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6072f-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6072f-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6072f-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6072f-200">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6072f-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6072f-202">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6072f-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6072f-204">a.</span><span class="sxs-lookup"><span data-stu-id="6072f-204">a.</span></span> <span data-ttu-id="6072f-205">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6072f-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6072f-206">b.</span><span class="sxs-lookup"><span data-stu-id="6072f-206">b.</span></span> <span data-ttu-id="6072f-207">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6072f-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6072f-208">c.</span><span class="sxs-lookup"><span data-stu-id="6072f-208">c.</span></span> <span data-ttu-id="6072f-209">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6072f-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6072f-210">d.</span><span class="sxs-lookup"><span data-stu-id="6072f-210">d.</span></span> <span data-ttu-id="6072f-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6072f-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="6072f-212">Creación de un usuario de prueba de Front</span><span class="sxs-lookup"><span data-stu-id="6072f-212">Create a Front test user</span></span>

<span data-ttu-id="6072f-213">En esta sección, creará un usuario llamado Britta Simon en Front.</span><span class="sxs-lookup"><span data-stu-id="6072f-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="6072f-214">Trabaje con el [equipo de soporte técnico al cliente de Front](mailto:support@frontapp.com) para agregar los usuarios a la plataforma de Front.</span><span class="sxs-lookup"><span data-stu-id="6072f-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="6072f-215">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6072f-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6072f-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6072f-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="6072f-217">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Front.</span><span class="sxs-lookup"><span data-stu-id="6072f-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="6072f-219">**Para asignar la usuaria Britta Simon a Front, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="6072f-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="6072f-220">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6072f-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6072f-222">En la lista de aplicaciones, seleccione **Front**.</span><span class="sxs-lookup"><span data-stu-id="6072f-222">In the applications list, select **Front**.</span></span>

    ![Vínculo a Front en la lista de aplicaciones](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="6072f-224">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6072f-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="6072f-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6072f-226">Click **Add** button.</span></span> <span data-ttu-id="6072f-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6072f-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="6072f-229">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6072f-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6072f-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6072f-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6072f-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6072f-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6072f-232">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="6072f-232">Test single sign-on</span></span>

<span data-ttu-id="6072f-233">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6072f-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="6072f-234">Al hacer clic en el icono de Front en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Front.</span><span class="sxs-lookup"><span data-stu-id="6072f-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6072f-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6072f-235">Additional resources</span></span>

* [<span data-ttu-id="6072f-236">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6072f-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6072f-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6072f-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

