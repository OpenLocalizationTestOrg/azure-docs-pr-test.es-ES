---
title: "Tutorial: Integración de Azure Active Directory con Datahug | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="2d92f-103">Tutorial: Integración de Azure Active Directory con Datahug</span><span class="sxs-lookup"><span data-stu-id="2d92f-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="2d92f-104">En este tutorial, obtendrá información sobre cómo integrar Datahug con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d92f-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d92f-105">La integración de Datahug con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2d92f-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2d92f-106">Puede controlar en Azure AD quién tiene acceso a Datahug.</span><span class="sxs-lookup"><span data-stu-id="2d92f-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="2d92f-107">Puede permitir que los usuarios inicien sesión automáticamente en Datahug (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d92f-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d92f-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2d92f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2d92f-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="2d92f-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="2d92f-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="2d92f-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d92f-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2d92f-111">Prerequisites</span></span>

<span data-ttu-id="2d92f-112">Para configurar la integración de Azure AD con Datahug, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2d92f-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="2d92f-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d92f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2d92f-114">Una suscripción habilitada para inicio de sesión único en Datahug</span><span class="sxs-lookup"><span data-stu-id="2d92f-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d92f-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2d92f-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d92f-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2d92f-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d92f-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2d92f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d92f-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d92f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d92f-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2d92f-119">Scenario description</span></span>
<span data-ttu-id="2d92f-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2d92f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d92f-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2d92f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d92f-122">Adición de Datahug desde la galería</span><span class="sxs-lookup"><span data-stu-id="2d92f-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="2d92f-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d92f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="2d92f-124">Adición de Datahug desde la galería</span><span class="sxs-lookup"><span data-stu-id="2d92f-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="2d92f-125">Para configurar la integración de Datahug en Azure AD, deberá agregar Datahug desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2d92f-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2d92f-126">**Para agregar Datahug desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2d92f-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2d92f-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d92f-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2d92f-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2d92f-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2d92f-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2d92f-134">En el cuadro de búsqueda, escriba **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-134">In the search box, type **Datahug**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="2d92f-136">En el panel de resultados, seleccione **Datahug** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d92f-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d92f-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d92f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d92f-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Datahug con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2d92f-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2d92f-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Datahug para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d92f-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="2d92f-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Datahug.</span><span class="sxs-lookup"><span data-stu-id="2d92f-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="2d92f-142">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Datahug.</span><span class="sxs-lookup"><span data-stu-id="2d92f-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="2d92f-143">Para configurar y probar el inicio de sesión único de Azure AD con Datahug, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2d92f-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2d92f-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2d92f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2d92f-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d92f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d92f-146">**[Creación de un usuario de prueba de Datahug](#creating-a-datahug-test-user)**: para tener un homólogo de Britta Simon en Datahug que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="2d92f-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d92f-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d92f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d92f-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2d92f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d92f-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d92f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d92f-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Datahug.</span><span class="sxs-lookup"><span data-stu-id="2d92f-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="2d92f-151">**Para configurar el inicio de sesión único de Azure AD con Datahug, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2d92f-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="2d92f-152">En Azure Portal, en la página de integración de la aplicación **Datahug**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2d92f-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2d92f-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="2d92f-156">En la sección **Dominio y direcciones URL de Datahug**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="2d92f-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="2d92f-158">a.</span><span class="sxs-lookup"><span data-stu-id="2d92f-158">a.</span></span> <span data-ttu-id="2d92f-159">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="2d92f-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="2d92f-160">b.</span><span class="sxs-lookup"><span data-stu-id="2d92f-160">b.</span></span> <span data-ttu-id="2d92f-161">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://apps.datahug.com/identity/<uniqueID>/acs`.</span><span class="sxs-lookup"><span data-stu-id="2d92f-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="2d92f-162">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2d92f-163">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="2d92f-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="2d92f-165">En el cuadro de texto **URL de inicio de sesión**, escriba una URL como: `https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="2d92f-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2d92f-166">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2d92f-166">These values are not the real.</span></span> <span data-ttu-id="2d92f-167">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="2d92f-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2d92f-168">Aquí le recomendamos que utilice el valor de cadena único en el identificador y la URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="2d92f-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="2d92f-169">Póngase en contacto con el [equipo de soporte técnico de Datahug](http://datahug.com/about/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="2d92f-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="2d92f-170">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2d92f-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="2d92f-172">Comprobar **Mostrar configuración avanzada de firma de certificados** y realizar los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2d92f-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="2d92f-174">a.</span><span class="sxs-lookup"><span data-stu-id="2d92f-174">a.</span></span> <span data-ttu-id="2d92f-175">En **Opciones de firma**, seleccione **Firmar aserción SAML**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="2d92f-176">b.</span><span class="sxs-lookup"><span data-stu-id="2d92f-176">b.</span></span> <span data-ttu-id="2d92f-177">En **Algoritmo de firma**, seleccione **SHA-1**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="2d92f-178">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2d92f-178">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="2d92f-180">En la sección **Configuración de Datahug**, haga clic en **Configurar Datahug** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2d92f-181">Copie **SAML Entity ID** y **SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="2d92f-183">Para configurar el inicio de sesión único en **Datahug**, debe enviar el **XML de metadatos**, **SAML Entity ID** (Identificador de entidad de SAML) y la **dirección URL de servicio de inicio de sesión de SAML** al [soporte técnico de Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="2d92f-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="2d92f-184">Ellos configuran esta aplicación para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="2d92f-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2d92f-185">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d92f-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2d92f-186">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2d92f-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2d92f-187">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d92f-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d92f-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d92f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d92f-189">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2d92f-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2d92f-191">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2d92f-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2d92f-192">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d92f-194">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d92f-196">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2d92f-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d92f-198">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2d92f-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d92f-200">a.</span><span class="sxs-lookup"><span data-stu-id="2d92f-200">a.</span></span> <span data-ttu-id="2d92f-201">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d92f-202">b.</span><span class="sxs-lookup"><span data-stu-id="2d92f-202">b.</span></span> <span data-ttu-id="2d92f-203">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d92f-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d92f-204">c.</span><span class="sxs-lookup"><span data-stu-id="2d92f-204">c.</span></span> <span data-ttu-id="2d92f-205">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2d92f-206">d.</span><span class="sxs-lookup"><span data-stu-id="2d92f-206">d.</span></span> <span data-ttu-id="2d92f-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="2d92f-208">Creación de un usuario de prueba de Datahug</span><span class="sxs-lookup"><span data-stu-id="2d92f-208">Creating a Datahug test user</span></span>

<span data-ttu-id="2d92f-209">Para permitir que los usuarios de Azure AD inicien sesión en Datahug, tienen que aprovisionarse en Datahug.</span><span class="sxs-lookup"><span data-stu-id="2d92f-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="2d92f-210">En Datahug, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2d92f-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="2d92f-211">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2d92f-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2d92f-212">Inicie sesión en su sitio de la compañía de Datahug como administrador.</span><span class="sxs-lookup"><span data-stu-id="2d92f-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="2d92f-213">Mantenga el puntero sobre el **engranaje** en la esquina superior derecha y haga clic en **Configuración**</span><span class="sxs-lookup"><span data-stu-id="2d92f-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![Agregar empleado](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="2d92f-215">Seleccione **Personas** y haga clic en la pestaña **Agregar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-215">Choose **People** and click the **Add Users** tab</span></span>

    ![Agregar empleado](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="2d92f-217">Escriba la dirección de correo electrónico de la persona para quien quiere crear una cuenta y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="2d92f-219">Puede enviar un correo electrónico de registro seleccionando la casilla de verificación **Send welcome email** (Enviar mensaje de correo de bienvenida).</span><span class="sxs-lookup"><span data-stu-id="2d92f-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="2d92f-220">Si está creando una cuenta para Salesforce, no envíe el mensaje de correo de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="2d92f-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2d92f-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d92f-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2d92f-222">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Datahug.</span><span class="sxs-lookup"><span data-stu-id="2d92f-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2d92f-224">**Para asignar a Britta Simon a Datahug, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2d92f-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="2d92f-225">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2d92f-227">En la lista de aplicaciones, seleccione **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-227">In the applications list, select **Datahug**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="2d92f-229">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2d92f-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-231">Click **Add** button.</span></span> <span data-ttu-id="2d92f-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2d92f-234">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2d92f-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2d92f-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d92f-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2d92f-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d92f-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2d92f-237">Testing single sign-on</span></span>

<span data-ttu-id="2d92f-238">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2d92f-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="2d92f-239">Al hacer clic en el icono de Datahug en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Datahug.</span><span class="sxs-lookup"><span data-stu-id="2d92f-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="2d92f-240">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="2d92f-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2d92f-241">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2d92f-241">Additional resources</span></span>

* [<span data-ttu-id="2d92f-242">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d92f-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d92f-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d92f-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

