---
title: "Tutorial: Integración de Azure Active Directory con Kronos | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="c7e3e-103">Tutorial: Integración de Azure Active Directory con Kronos</span><span class="sxs-lookup"><span data-stu-id="c7e3e-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="c7e3e-104">En este tutorial, obtendrá información sobre cómo integrar Kronos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7e3e-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7e3e-105">La integración de Kronos con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7e3e-106">Puede controlar en Azure AD quién tiene acceso a Kronos</span><span class="sxs-lookup"><span data-stu-id="c7e3e-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="c7e3e-107">Puede permitir que los usuarios inicien sesión automáticamente en Kronos (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7e3e-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7e3e-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7e3e-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7e3e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7e3e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c7e3e-110">Prerequisites</span></span>

<span data-ttu-id="c7e3e-111">Para configurar la integración de Azure AD con Kronos, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="c7e3e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7e3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7e3e-113">Una suscripción habilitada para el SSO en **Kronos Workforce Central**</span><span class="sxs-lookup"><span data-stu-id="c7e3e-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7e3e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7e3e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7e3e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7e3e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7e3e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7e3e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c7e3e-118">Scenario description</span></span>
<span data-ttu-id="c7e3e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7e3e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7e3e-121">Adición de Kronos desde la galería</span><span class="sxs-lookup"><span data-stu-id="c7e3e-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="c7e3e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7e3e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="c7e3e-123">Adición de Kronos desde la galería</span><span class="sxs-lookup"><span data-stu-id="c7e3e-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="c7e3e-124">Para configurar la integración de Kronos en Azure AD, deberá agregar Kronos desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7e3e-125">**Para agregar Kronos desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c7e3e-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7e3e-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7e3e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7e3e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c7e3e-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c7e3e-133">En el cuadro de búsqueda, escriba **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-133">In the search box, type **Kronos**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="c7e3e-135">En el panel de resultados, seleccione **Kronos** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7e3e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7e3e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7e3e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kronos con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c7e3e-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7e3e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Kronos para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="c7e3e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Kronos.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="c7e3e-141">Para establecer la relación de vínculo, en Kronos, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c7e3e-142">Para configurar y probar el inicio de sesión único de Azure AD con Kronos, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7e3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7e3e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7e3e-145">**[Creación de un usuario de prueba de Kronos](#creating-a-kronos-test-user)**: para tener un homólogo de Britta Simon en Kronos que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7e3e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7e3e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7e3e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7e3e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7e3e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Kronos.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="c7e3e-150">**Para configurar el inicio de sesión único de Azure AD con Kronos, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c7e3e-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="c7e3e-151">En Azure Portal, en la página de integración de la aplicación **Kronos**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c7e3e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="c7e3e-155">En la sección **Dominio y direcciones URL de Kronos**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="c7e3e-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-157">a.</span></span> <span data-ttu-id="c7e3e-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="c7e3e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="c7e3e-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-159">b.</span></span> <span data-ttu-id="c7e3e-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7e3e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-161">These values are not real.</span></span> <span data-ttu-id="c7e3e-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="c7e3e-163">Póngase en contacto con [equipo de soporte técnico de Kronos](https://www.kronos.in/contact/en-in/form) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="c7e3e-164">La aplicación Kronos espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c7e3e-165">Trabaje primero con el [equipo de soporte técnico de Kronos](https://www.kronos.in/contact/en-in/form) para identificar el identificador de usuario correcto que se asignará a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="c7e3e-166">También siga sus instrucciones sobre el atributo que desean usar para esta asignación.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="c7e3e-167">Microsoft recomienda utilizar el atributo **"NameIdentifier"** como identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="c7e3e-168">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="c7e3e-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="c7e3e-170">Aquí hemos asignado el **identificador de usuario (identificador de nombre)** con la función **ExtractMailPrefix()** de **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="c7e3e-171">Esto da como resultado el valor de prefijo del correo electrónico del usuario que es el identificador de usuario único.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="c7e3e-172">Este se envía a la aplicación Kronos con cada respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Configurar inicio de sesión único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="c7e3e-174">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="c7e3e-175">a.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-175">a.</span></span> <span data-ttu-id="c7e3e-176">En la lista desplegable Identificador de usuario, seleccione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="c7e3e-177">b.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-177">b.</span></span> <span data-ttu-id="c7e3e-178">En la lista desplegable **Correo**, seleccione **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="c7e3e-179">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="c7e3e-181">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c7e3e-181">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c7e3e-183">Para configurar el inicio de sesión único en el lado de **Kronos**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="c7e3e-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="c7e3e-184">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7e3e-185">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7e3e-186">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7e3e-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7e3e-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7e3e-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7e3e-188">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c7e3e-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c7e3e-190">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c7e3e-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7e3e-191">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7e3e-193">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7e3e-195">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7e3e-197">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c7e3e-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7e3e-199">a.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-199">a.</span></span> <span data-ttu-id="c7e3e-200">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7e3e-201">b.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-201">b.</span></span> <span data-ttu-id="c7e3e-202">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7e3e-203">c.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-203">c.</span></span> <span data-ttu-id="c7e3e-204">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7e3e-205">d.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-205">d.</span></span> <span data-ttu-id="c7e3e-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="c7e3e-207">Creación de un usuario de prueba de Kronos</span><span class="sxs-lookup"><span data-stu-id="c7e3e-207">Creating a Kronos test user</span></span>

<span data-ttu-id="c7e3e-208">En esta sección, creará un usuario llamado Britta Simon en Kronos.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="c7e3e-209">La aplicación Kronos necesita que todos los usuarios estén aprovisionados en la aplicación antes de realizar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="c7e3e-210">Trabaje con el [servicio de soporte técnico al cliente de Kronos](https://www.kronos.in/contact/en-in/form) para aprovisionar todos estos usuarios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7e3e-211">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7e3e-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7e3e-212">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Kronos.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c7e3e-214">**Para asignar Britta Simon a Kronos, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c7e3e-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="c7e3e-215">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c7e3e-217">En la lista de aplicaciones, seleccione **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-217">In the applications list, select **Kronos**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="c7e3e-219">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c7e3e-221">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-221">Click **Add** button.</span></span> <span data-ttu-id="c7e3e-222">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c7e3e-224">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7e3e-225">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7e3e-226">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7e3e-227">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c7e3e-227">Testing single sign-on</span></span>

<span data-ttu-id="c7e3e-228">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c7e3e-229">Al hacer clic en el icono de Kronos en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Kronos.</span><span class="sxs-lookup"><span data-stu-id="c7e3e-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7e3e-230">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c7e3e-230">Additional resources</span></span>

* [<span data-ttu-id="c7e3e-231">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7e3e-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7e3e-232">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7e3e-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

