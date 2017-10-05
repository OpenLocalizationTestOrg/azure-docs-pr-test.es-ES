---
title: "Tutorial: Integración de Azure Active Directory con Qlik Sense Enterprise | Microsoft Doc"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Qlik Sense Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="b4535-103">Tutorial: Integración de Azure Active Directory con Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="b4535-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="b4535-104">En este tutorial, aprenderá a integrar Qlik Sense Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4535-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4535-105">La integración de Qlik Sense Enterprise con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b4535-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b4535-106">Puede controlar en Azure AD quién tiene acceso a Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b4535-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="b4535-107">Puede permitir que los usuarios inicien sesión automáticamente en Qlik Sense Enterprise (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b4535-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b4535-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b4535-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4535-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4535-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b4535-110">Prerequisites</span></span>

<span data-ttu-id="b4535-111">Para configurar la integración de Azure AD con Qlik Sense Enterprise, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b4535-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="b4535-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4535-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b4535-113">Una suscripción habilitada para el inicio de sesión único en Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="b4535-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4535-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b4535-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4535-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b4535-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4535-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b4535-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4535-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4535-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4535-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b4535-118">Scenario description</span></span>
<span data-ttu-id="b4535-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b4535-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4535-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b4535-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4535-121">Adición de Qlik Sense Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="b4535-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="b4535-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4535-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="b4535-123">Adición de Qlik Sense Enterprise desde la galería</span><span class="sxs-lookup"><span data-stu-id="b4535-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="b4535-124">Para configurar la integración de Qlik Sense Enterprise en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b4535-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b4535-125">**Para agregar Qlik Sense Enterprise desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b4535-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b4535-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b4535-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="b4535-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b4535-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b4535-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b4535-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="b4535-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b4535-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="b4535-133">En el cuadro de búsqueda, escriba **Qlik Sense Enterprise**, seleccione **Qlik Sense Enterprise** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4535-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Qlik Sense Enterprise en la lista de resultados](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b4535-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4535-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b4535-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Qlik Sense Enterprise utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b4535-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4535-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Qlik Sense Enterprise para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="b4535-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b4535-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="b4535-139">Para establecer la relación de vínculo, en Qlik Sense Enterprise, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b4535-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b4535-140">Para configurar y probar el inicio de sesión único de Azure AD con Qlik Sense Enterprise, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b4535-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b4535-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="b4535-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b4535-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4535-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4535-143">**[Creación de un usuario de prueba de Qlik Sense Enterprise](#create-a-qlik-sense-enterprise-test-user)**: para tener un homólogo de Britta Simon en Qlik Sense Enterprise que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b4535-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4535-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="b4535-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b4535-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4535-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b4535-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b4535-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="b4535-148">**Para configurar el inicio de sesión único de Azure AD con Qlik Sense Enterprise, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b4535-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="b4535-149">En la página de integración de la aplicación **Qlik Sense Enterprise** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b4535-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="b4535-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b4535-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="b4535-153">En la sección **Dominio y direcciones URL de Qlik Sense Enterprise**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b4535-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="b4535-155">a.</span><span class="sxs-lookup"><span data-stu-id="b4535-155">a.</span></span> <span data-ttu-id="b4535-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`.</span><span class="sxs-lookup"><span data-stu-id="b4535-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b4535-157">No se olvide de escribir la barra diagonal al final de este URI,</span><span class="sxs-lookup"><span data-stu-id="b4535-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="b4535-158">ya que es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="b4535-158">It is required.</span></span>
    
    <span data-ttu-id="b4535-159">b.</span><span class="sxs-lookup"><span data-stu-id="b4535-159">b.</span></span> <span data-ttu-id="b4535-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="b4535-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="b4535-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="b4535-161">These values are not real.</span></span> <span data-ttu-id="b4535-162">Actualice estos valores con el identificador y dirección URL de inicio de sesión reales, que se explican más adelante en el tutorial o póngase en contacto con el [equipo de soporte técnico de Qlik Sense Enterprise](https://www.qlik.com/us/services/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="b4535-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="b4535-163">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b4535-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="b4535-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b4535-165">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b4535-167">Prepare el archivo XML de metadatos de federación para que pueda cargarse en el servidor de Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="b4535-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="b4535-168">Antes de cargar los metadatos de IdP en el servidor de Qlik Sense, hay que editar el archivo para quitar información y, de este modo, garantizar que la conexión entre Azure AD y el servidor de Qlik se realice sin problemas.</span><span class="sxs-lookup"><span data-stu-id="b4535-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="b4535-170">a.</span><span class="sxs-lookup"><span data-stu-id="b4535-170">a.</span></span> <span data-ttu-id="b4535-171">Abra el archivo FederationMetaData.xml que ha descargado de Azure Portal en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b4535-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="b4535-172">b.</span><span class="sxs-lookup"><span data-stu-id="b4535-172">b.</span></span> <span data-ttu-id="b4535-173">Busque el valor **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="b4535-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="b4535-174">Hay cuatro entradas (dos pares de etiquetas de elementos de apertura y cierre).</span><span class="sxs-lookup"><span data-stu-id="b4535-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="b4535-175">c.</span><span class="sxs-lookup"><span data-stu-id="b4535-175">c.</span></span> <span data-ttu-id="b4535-176">Elimine del archivo las etiquetas de RoleDescriptor y toda la información intermedia.</span><span class="sxs-lookup"><span data-stu-id="b4535-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="b4535-177">d.</span><span class="sxs-lookup"><span data-stu-id="b4535-177">d.</span></span> <span data-ttu-id="b4535-178">Guarde el archivo y téngalo a mano, ya que vamos a utilizarlo más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="b4535-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="b4535-179">Acceda a Qlik Sense Qlik Management Console (QMC) como un usuario que pueda crear configuraciones de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="b4535-180">En la consola QMC, haga clic en el elemento de menú **Virtual Proxies** (servidores proxy virtuales).</span><span class="sxs-lookup"><span data-stu-id="b4535-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="b4535-182">Haga clic en el botón **Create new** (Crear nuevo) situado en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="b4535-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="b4535-184">Aparece la pantalla de edición Virtual Proxy (Proxy virtual).</span><span class="sxs-lookup"><span data-stu-id="b4535-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="b4535-185">En la parte derecha de la pantalla hay un menú con el que puede hacer que se muestren las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="b4535-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="b4535-187">Active la opción de menú Identificación y escriba la información de identificación de la configuración de proxy virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4535-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="b4535-189">a.</span><span class="sxs-lookup"><span data-stu-id="b4535-189">a.</span></span> <span data-ttu-id="b4535-190">El campo **Description** (Descripción) es un nombre descriptivo de la configuración del proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="b4535-191">Escriba un valor para este campo.</span><span class="sxs-lookup"><span data-stu-id="b4535-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="b4535-192">b.</span><span class="sxs-lookup"><span data-stu-id="b4535-192">b.</span></span> <span data-ttu-id="b4535-193">El campo **Prefix** (Prefijo) identifica el punto de conexión del proxy virtual para conectarse a Qlik Sense con el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="b4535-194">Escriba un nombre de prefijo único para este proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="b4535-195">c.</span><span class="sxs-lookup"><span data-stu-id="b4535-195">c.</span></span> <span data-ttu-id="b4535-196">**Session inactivity timeout (minutes)** (Tiempo de espera de inactividad de la sesión [minutos]) es el tiempo de espera de las conexiones que se establecen a través de este proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="b4535-197">d.</span><span class="sxs-lookup"><span data-stu-id="b4535-197">d.</span></span> <span data-ttu-id="b4535-198">**Session cookie header name** (Nombre de encabezado de cookie de sesión) es el nombre de la cookie que almacena el identificador de la sesión de Qlik Sense que recibe un usuario tras autenticarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="b4535-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="b4535-199">Este nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="b4535-199">This name must be unique.</span></span>

12. <span data-ttu-id="b4535-200">Haga clic en la opción de menú Autenticación para que se muestre.</span><span class="sxs-lookup"><span data-stu-id="b4535-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="b4535-201">Aparecerá la pantalla Autenticación.</span><span class="sxs-lookup"><span data-stu-id="b4535-201">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="b4535-203">a.</span><span class="sxs-lookup"><span data-stu-id="b4535-203">a.</span></span> <span data-ttu-id="b4535-204">El menú desplegable **Anonymous access mode** (Modo de acceso anónimo) determina si los usuarios anónimos pueden acceder a Qlik Sense a través del proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="b4535-205">La opción predeterminada es No anonymous user (Ningún usuario anónimo).</span><span class="sxs-lookup"><span data-stu-id="b4535-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="b4535-206">b.</span><span class="sxs-lookup"><span data-stu-id="b4535-206">b.</span></span> <span data-ttu-id="b4535-207">El menú desplegable **Authentication method** (Método de autenticación) determina el esquema de autenticación que utilizará el proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="b4535-208">Seleccione SAML en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b4535-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="b4535-209">Como resultado, aparecerán más opciones.</span><span class="sxs-lookup"><span data-stu-id="b4535-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="b4535-210">c.</span><span class="sxs-lookup"><span data-stu-id="b4535-210">c.</span></span> <span data-ttu-id="b4535-211">En el campo **SAML host URI**(identificador URI de host SAML), especifique el nombre de host que tendrán que escribir los usuarios para acceder a Qlik Sense a través de este proxy virtual de SAML.</span><span class="sxs-lookup"><span data-stu-id="b4535-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="b4535-212">El nombre de host es el URI del servidor de Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="b4535-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="b4535-213">d.</span><span class="sxs-lookup"><span data-stu-id="b4535-213">d.</span></span> <span data-ttu-id="b4535-214">En el campo **SAML entity ID** (Id. de entidad SAML), escriba el mismo valor que especificó en el campo de URI de host SAML.</span><span class="sxs-lookup"><span data-stu-id="b4535-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="b4535-215">e.</span><span class="sxs-lookup"><span data-stu-id="b4535-215">e.</span></span> <span data-ttu-id="b4535-216">**SAML IdP metadata** (Metadatos de IdP de SAML) es el archivo que se editó anteriormente en la sección de **modificación de los metadatos de federación desde la configuración de Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="b4535-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="b4535-217">**Antes de cargar los metadatos de IdP, hay que editar el archivo** para quitar información y, de este modo, garantizar que la conexión entre Azure AD y el servidor de Qlik se realice sin problemas.</span><span class="sxs-lookup"><span data-stu-id="b4535-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="b4535-218">**Consulte las instrucciones anteriores si aún no ha modificado el archivo.**</span><span class="sxs-lookup"><span data-stu-id="b4535-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="b4535-219">Si ya lo ha hecho, haga clic en el botón Examinar y seleccione el archivo de metadatos editado para cargarlo en la configuración de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="b4535-220">f.</span><span class="sxs-lookup"><span data-stu-id="b4535-220">f.</span></span> <span data-ttu-id="b4535-221">Escriba el nombre de atributo o la referencia de esquema del atributo SAML que representa el **UserID** (identificador de usuario) que Azure AD enviará al servidor de Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="b4535-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="b4535-222">La información de referencia del esquema está disponible en las pantallas de la aplicación de Azure que aparecen tras el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="b4535-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="b4535-223">Para usar el atributo name, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="b4535-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="b4535-224">g.</span><span class="sxs-lookup"><span data-stu-id="b4535-224">g.</span></span> <span data-ttu-id="b4535-225">Escriba el valor del **directorio de usuarios** que se asociará a los usuarios cuando se autentiquen en el servidor de Qlik Sense a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="b4535-226">Los valores codificados deben estar entre **corchetes**.</span><span class="sxs-lookup"><span data-stu-id="b4535-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="b4535-227">Para utilizar un atributo enviado en la aserción SAML de Azure AD, escriba el nombre del atributo en este cuadro de texto **sin** corchetes.</span><span class="sxs-lookup"><span data-stu-id="b4535-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="b4535-228">h.</span><span class="sxs-lookup"><span data-stu-id="b4535-228">h.</span></span> <span data-ttu-id="b4535-229">El **algoritmo de firma SAML** establece la firma de certificados del proveedor de servicios (en este caso, el servidor de Qlik Sense) en la configuración de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="b4535-230">Si el servidor de Qlik Sense utiliza un certificado de confianza generado mediante el proveedor de servicios criptográficos AES y RSA mejorado de Microsoft, cambie el algoritmo de firma SAML a **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="b4535-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="b4535-231">i.</span><span class="sxs-lookup"><span data-stu-id="b4535-231">i.</span></span> <span data-ttu-id="b4535-232">La sección de asignación de atributos SAML permite enviar otros atributos, como grupos, a Qlik Sense para utilizarse en reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b4535-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="b4535-233">Haga clic en la opción de menú **LOAD BALANCING** (Equilibrio de carga) para que se muestre.</span><span class="sxs-lookup"><span data-stu-id="b4535-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="b4535-234">Aparecerá la pantalla Equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="b4535-234">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="b4535-236">Haga clic en el botón **Add new server node** (Agregar nuevo nodo de servidor), seleccione los nodos de motor a los que Qlik Sense enviará sesiones para equilibrar la carga y, luego, haga clic en el botón **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="b4535-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="b4535-238">Haga clic en la opción de menú Opciones avanzadas para que se muestre.</span><span class="sxs-lookup"><span data-stu-id="b4535-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="b4535-239">Aparece la pantalla Opciones avanzadas.</span><span class="sxs-lookup"><span data-stu-id="b4535-239">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="b4535-241">La lista blanca de Host identifica los nombres de host que se aceptan al conectarse al servidor de Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="b4535-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="b4535-242">**Escriba el nombre de host que especificarán los usuarios al conectarse al servidor de Qlik sentido.**</span><span class="sxs-lookup"><span data-stu-id="b4535-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="b4535-243">El nombre de host es el mismo valor que el URI de host SAML, pero sin "https://".</span><span class="sxs-lookup"><span data-stu-id="b4535-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="b4535-244">Haga clic en el botón **Apply** (Aplicar).</span><span class="sxs-lookup"><span data-stu-id="b4535-244">Click the **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="b4535-246">Haga clic en Aceptar para aceptar el mensaje de advertencia que indica que se reiniciará el proxy vinculado al proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="b4535-248">En la parte derecha de la pantalla, aparece el menú de elementos Asociado.</span><span class="sxs-lookup"><span data-stu-id="b4535-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="b4535-249">Haga clic en la opción de menú **Proxies** (Servidores proxy).</span><span class="sxs-lookup"><span data-stu-id="b4535-249">Click on the **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="b4535-251">Aparecerá la pantalla Servidores proxy.</span><span class="sxs-lookup"><span data-stu-id="b4535-251">The proxy screen appears.</span></span>  <span data-ttu-id="b4535-252">Haga clic en el botón **Link** (Vincular) de la parte inferior para vincular un proxy al proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="b4535-254">Seleccione el nodo de proxy que admitirá esta conexión de proxy virtual y haga clic en el botón **Link** (Vincular).</span><span class="sxs-lookup"><span data-stu-id="b4535-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="b4535-255">Cuando termine el proceso de vinculación, el proxy aparecerá debajo de los servidores proxy asociados.</span><span class="sxs-lookup"><span data-stu-id="b4535-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="b4535-258">Cuando pasen entre unos cinco y diez segundos, se mostrará el mensaje Actualizar QMC.</span><span class="sxs-lookup"><span data-stu-id="b4535-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="b4535-259">Haga clic en el botón **Refresh QMC** (Actualizar QMC).</span><span class="sxs-lookup"><span data-stu-id="b4535-259">Click the **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="b4535-261">Cuando se actualice la consola QMC, haga clic en el elemento de menú **Virtual proxies** (Servidores proxy virtuales).</span><span class="sxs-lookup"><span data-stu-id="b4535-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="b4535-262">La nueva entrada SAML virtual proxy (Proxy virtual de SAML) se muestra en la tabla que aparece en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="b4535-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="b4535-263">Haga clic en la entrada de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="b4535-263">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="b4535-265">En la parte inferior de la pantalla, se activará el botón Download SP metadata (Descargar metadatos de SP).</span><span class="sxs-lookup"><span data-stu-id="b4535-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="b4535-266">Haga clic en el botón **Download SP metadata** (Descargar metadatos de SP) para guardar los metadatos en un archivo.</span><span class="sxs-lookup"><span data-stu-id="b4535-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="b4535-268">Abra el archivo de metadatos de SP.</span><span class="sxs-lookup"><span data-stu-id="b4535-268">Open the sp metadata file.</span></span>  <span data-ttu-id="b4535-269">Observe las entradas **entityID** y **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="b4535-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="b4535-270">Estos valores son equivalentes a los de **Identificador** y **Dirección URL de inicio de sesión** de la configuración de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="b4535-271">Pegue estos valores en la sección **Dominio y direcciones URL de Qlik Sense Enterprise** en la configuración de la aplicación de Azure AD; si no coinciden, se deben reemplazar en el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4535-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="b4535-273">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4535-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b4535-274">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b4535-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b4535-275">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4535-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b4535-276">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4535-276">Create an Azure AD test user</span></span>
<span data-ttu-id="b4535-277">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b4535-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="b4535-279">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b4535-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b4535-280">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b4535-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![Botón Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b4535-282">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b4535-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b4535-284">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b4535-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![Botón Agregar](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b4535-286">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b4535-286">In the **User** dialog box, perform the following steps:</span></span>

   ![Cuadro de diálogo Usuario](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="b4535-288">a.</span><span class="sxs-lookup"><span data-stu-id="b4535-288">a.</span></span> <span data-ttu-id="b4535-289">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4535-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="b4535-290">b.</span><span class="sxs-lookup"><span data-stu-id="b4535-290">b.</span></span> <span data-ttu-id="b4535-291">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4535-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="b4535-292">c.</span><span class="sxs-lookup"><span data-stu-id="b4535-292">c.</span></span> <span data-ttu-id="b4535-293">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b4535-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="b4535-294">d.</span><span class="sxs-lookup"><span data-stu-id="b4535-294">d.</span></span> <span data-ttu-id="b4535-295">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b4535-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="b4535-296">Creación de un usuario de prueba de Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="b4535-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="b4535-297">En esta sección, creará un usuario llamado "Britta Simon" en Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b4535-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="b4535-298">Colabore con el [equipo de soporte técnico de Qlik Sense Enterprise](https://www.qlik.com/us/services/support) para agregar los usuarios en la plataforma Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b4535-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="b4535-299">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b4535-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b4535-300">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4535-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="b4535-301">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b4535-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="b4535-303">**Para asignar el usuario Britta Simon a Qlik Sense Enterprise, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b4535-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="b4535-304">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b4535-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b4535-306">En la lista de aplicaciones, seleccione **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="b4535-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![Vínculo a Qlik Sense Enterprise en la lista de aplicaciones](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="b4535-308">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b4535-308">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="b4535-310">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b4535-310">Click **Add** button.</span></span> <span data-ttu-id="b4535-311">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b4535-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="b4535-313">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b4535-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b4535-314">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b4535-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b4535-315">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b4535-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b4535-316">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="b4535-316">Test single sign-on</span></span>

<span data-ttu-id="b4535-317">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4535-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b4535-318">Al hacer clic en el icono de Qlik Sense Enterprise del panel de acceso, debería iniciar sesión automáticamente en la aplicación Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b4535-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b4535-319">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b4535-319">Additional resources</span></span>

* [<span data-ttu-id="b4535-320">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4535-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4535-321">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4535-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

