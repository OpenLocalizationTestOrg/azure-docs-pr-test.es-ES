---
title: "Tutorial: Integración de Azure Active Directory con Cisco Spark | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="1b7d9-103">Tutorial: integración de Azure Active Directory con Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="1b7d9-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="1b7d9-104">En este tutorial, aprenderá a integrar Cisco Spark con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b7d9-105">Integrar Cisco Spark con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1b7d9-106">Puede controlar en Azure AD quién tiene acceso a Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="1b7d9-107">Puede permitir que los usuarios inicien sesión automáticamente en Cisco Spark (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b7d9-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1b7d9-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b7d9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1b7d9-110">Prerequisites</span></span>

<span data-ttu-id="1b7d9-111">Para configurar la integración de Azure AD con Cisco Spark, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="1b7d9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b7d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b7d9-113">Una suscripción habilitada para el inicio de sesión único en Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="1b7d9-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b7d9-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b7d9-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b7d9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b7d9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b7d9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1b7d9-118">Scenario description</span></span>
<span data-ttu-id="1b7d9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b7d9-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b7d9-121">Adición de Cisco Spark desde la galería</span><span class="sxs-lookup"><span data-stu-id="1b7d9-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="1b7d9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b7d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="1b7d9-123">Adición de Cisco Spark desde la galería</span><span class="sxs-lookup"><span data-stu-id="1b7d9-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="1b7d9-124">Para configurar la integración de Cisco Spark en Azure AD, será preciso que agregue Cisco Spark desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b7d9-125">**Para agregar Cisco Spark desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1b7d9-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b7d9-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1b7d9-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1b7d9-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1b7d9-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1b7d9-133">En el cuadro de búsqueda, escriba **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-133">In the search box, type **Cisco Spark**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="1b7d9-135">En el panel de resultados, seleccione **Cisco Spark** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b7d9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b7d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b7d9-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Cisco Spark con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1b7d9-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1b7d9-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Cisco Spark para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="1b7d9-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="1b7d9-141">Para establecer la relación de vínculo, en Cisco Spark, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1b7d9-142">Para configurar y probar el inicio de sesión único de Azure AD con Cisco Spark, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b7d9-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1b7d9-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b7d9-145">**[Creación de un usuario de prueba de Cisco Spark](#creating-a-cisco-spark-test-user)**: para tener un homólogo de Britta Simon en Cisco Spark que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b7d9-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b7d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b7d9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b7d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b7d9-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="1b7d9-150">**Para configurar el inicio de sesión único de Azure AD con Cisco Spark, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1b7d9-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="1b7d9-151">En Azure Portal, en la página de integración de la aplicación **Cisco Spark**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1b7d9-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="1b7d9-155">En la sección **Dominio y direcciones URL de Cisco Spark**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="1b7d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-157">a.</span></span> <span data-ttu-id="1b7d9-158">En el cuadro de texto **URL de inicio de sesión**, escriba una URL como: `https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="1b7d9-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="1b7d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-159">b.</span></span> <span data-ttu-id="1b7d9-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1b7d9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1b7d9-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-161">This value is not real.</span></span> <span data-ttu-id="1b7d9-162">Actualícelo con el identificador real.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="1b7d9-163">Póngase en contacto con el [equipo de soporte técnico de Cisco Spark](https://support.ciscospark.com/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="1b7d9-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="1b7d9-166">La aplicación de Cisco Spark espera que las aserciones SAML contengan atributos específicos.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="1b7d9-167">Configure los siguientes atributos para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="1b7d9-168">Puede administrar los valores de estos atributos en la sección **Atributos de usuario** de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="1b7d9-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-169">The following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="1b7d9-171">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="1b7d9-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="1b7d9-172">Attribute Name</span></span>  | <span data-ttu-id="1b7d9-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="1b7d9-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="1b7d9-174">uid</span><span class="sxs-lookup"><span data-stu-id="1b7d9-174">uid</span></span>    | <span data-ttu-id="1b7d9-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1b7d9-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="1b7d9-176">a.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-176">a.</span></span> <span data-ttu-id="1b7d9-177">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="1b7d9-180">b.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-180">b.</span></span> <span data-ttu-id="1b7d9-181">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1b7d9-182">c.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-182">c.</span></span> <span data-ttu-id="1b7d9-183">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1b7d9-184">d.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-184">d.</span></span> <span data-ttu-id="1b7d9-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-185">Click **Ok**.</span></span>

7. <span data-ttu-id="1b7d9-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1b7d9-186">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1b7d9-188">Inicie sesión en [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) (Administración de colaboración en la nube de Cisco) con sus credenciales completas de administrador.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="1b7d9-189">Seleccione **Settings** (Configuración) y en la sección **Authentication** (Autenticación), haga clic en **Modify** (Modificar).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="1b7d9-191">Seleccione **Integrate a 3rd-party identity provider. (Advanced)** (Integrar un proveedor de identidades de terceros [avanzado]).y vaya a la pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="1b7d9-192">En la página **Import Idp Metadata** (Importar metadatos de LDP) arrastre y coloque el archivo de metadatos de Azure AD en la página o utilice la opción de explorador de archivos para buscar y cargar el archivo de metadatos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="1b7d9-193">Después, seleccione **Require certificate signed by a certificate authority in Metadata (more secure)** (Requerir certificado firmado por una entidad de certificación en metadatos [más seguro]) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="1b7d9-195">Seleccione **Test SSO Connection** (Probar SSO de conexión) y cuando se abra una nueva pestaña de explorador, autentíquese con Azure AD mediante el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="1b7d9-196">Vuelva a la pestaña del explorador de **Cisco Cloud Collaboration Management**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="1b7d9-197">Si la prueba se realizó correctamente, seleccione **This test was successful. Enable Single Sign-On option** (Esta prueba se realizó correctamente. Habilite la opción de inicio de sesión único) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="1b7d9-198">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1b7d9-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1b7d9-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b7d9-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b7d9-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b7d9-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b7d9-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1b7d9-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1b7d9-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1b7d9-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b7d9-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b7d9-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b7d9-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b7d9-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b7d9-213">a.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-213">a.</span></span> <span data-ttu-id="1b7d9-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b7d9-215">b.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-215">b.</span></span> <span data-ttu-id="1b7d9-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b7d9-217">c.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-217">c.</span></span> <span data-ttu-id="1b7d9-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1b7d9-219">d.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-219">d.</span></span> <span data-ttu-id="1b7d9-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="1b7d9-221">Creación de un usuario de prueba de Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="1b7d9-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="1b7d9-222">En esta sección, creará un usuario llamado Britta Simon en Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="1b7d9-223">En esta sección, creará un usuario llamado Britta Simon en Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="1b7d9-224">Vaya a [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) con sus credenciales de administración completas.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="1b7d9-225">Haga clic en **Usuarios** y después en **Administrar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="1b7d9-227">En la ventana **Manage User** (Administrar usuario), seleccione **Manually add or modify users** (Agregar o modificar usuarios manualmente) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="1b7d9-228">Seleccione **Names and Email address** (Nombres y direcciones de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-228">Select **Names and Email address**.</span></span> <span data-ttu-id="1b7d9-229">Después, rellene el cuadro de texto de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b7d9-229">Then, fill out the textbox as follows:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="1b7d9-231">a.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-231">a.</span></span> <span data-ttu-id="1b7d9-232">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="1b7d9-233">b.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-233">b.</span></span> <span data-ttu-id="1b7d9-234">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="1b7d9-235">c.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-235">c.</span></span> <span data-ttu-id="1b7d9-236">En el cuadro de texto **Dirección de correo electrónico**, escriba **britta.simon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="1b7d9-237">Haga clic en el signo más para agregar a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="1b7d9-238">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="1b7d9-239">En la ventana **Add Services for Users** (Agregar servicios para los usuarios), haga clic en **Save** (Guardar) y después en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="1b7d9-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1b7d9-240">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b7d9-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1b7d9-241">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1b7d9-243">**Para asignar a Britta Simon a Cisco Spark, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1b7d9-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="1b7d9-244">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1b7d9-246">En la lista de aplicaciones, seleccione **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="1b7d9-248">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1b7d9-250">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-250">Click **Add** button.</span></span> <span data-ttu-id="1b7d9-251">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1b7d9-253">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1b7d9-254">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b7d9-255">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b7d9-256">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1b7d9-256">Testing single sign-on</span></span>

<span data-ttu-id="1b7d9-257">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1b7d9-258">Al hacer clic en el icono de Cisco Spark en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="1b7d9-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b7d9-259">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1b7d9-259">Additional resources</span></span>

* [<span data-ttu-id="1b7d9-260">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b7d9-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b7d9-261">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b7d9-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

