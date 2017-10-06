---
title: "Tutorial: Integración de Azure Active Directory con SAP Business Object Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la nube de objeto de negocios de SAP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="d7a0f-103">Tutorial: Integración de Azure Active Directory con SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="d7a0f-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="d7a0f-104">En este tutorial, aprenderá cómo toointegrate SAP Business objeto en la nube con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7a0f-105">Obtener hello las siguientes ventajas cuando se integre SAP Business objeto en la nube con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="d7a0f-106">En Azure AD, puede controlar quién tiene acceso tooSAP nube del objeto de negocios.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="d7a0f-107">Puede firmar automáticamente en su tooSAP de los usuarios empresariales objeto nube mediante el inicio de sesión único y una cuenta de usuario Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="d7a0f-108">Puede administrar las cuentas en una ubicación central, Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="d7a0f-109">toolearn más información acerca del software como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7a0f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d7a0f-110">Prerequisites</span></span>

<span data-ttu-id="d7a0f-111">tooset la integración de Azure AD con la nube de objeto de negocios de SAP, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="d7a0f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7a0f-113">Una instancia de SAP Business Object Cloud con el inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="d7a0f-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="d7a0f-114">Si prueba a pasos de hello en este tutorial, se recomienda que no probarlas en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="d7a0f-115">Recomendaciones para probar los pasos de hello en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="d7a0f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="d7a0f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba gratuita durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7a0f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d7a0f-118">Scenario description</span></span>
<span data-ttu-id="d7a0f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="d7a0f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7a0f-121">Agregar objeto nube de SAP Business de hello Galería.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="d7a0f-122">Configuración y prueba del inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="d7a0f-123">Agregar objeto nube de SAP Business de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d7a0f-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="d7a0f-124">tooset la integración de Hola de SAP Business objeto en la nube con Azure AD, en la Galería de hello, agregue la lista de tooyour de SAP Business objeto nube de las aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7a0f-125">en la nube SAP Business objeto desde la Galería de Hola tooadd:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="d7a0f-126">Hola [portal de Azure](https://portal.azure.com), en el menú de la izquierda de Hola, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="d7a0f-128">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![página de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="d7a0f-130">tooadd una nueva aplicación, seleccione **nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-130">tooadd a new application, select **New application**.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="d7a0f-132">En el cuadro de búsqueda de hello, escriba **SAP Business objeto nube**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![cuadro de búsqueda de Hola](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="d7a0f-134">En el panel de resultados de hello, seleccione **SAP Business objeto nube**y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![Lista de resultados de la nube de objeto de negocios SAP en hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d7a0f-136">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a0f-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="d7a0f-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con SAP Business Object Cloud mediante un usuario de prueba llamado *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="d7a0f-138">Para toowork de inicio de sesión único, Azure AD necesita usuario de equivalente de Azure AD tooknow hello en la nube de objeto de negocios de SAP.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="d7a0f-139">Se debe establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en la nube de objeto de negocios de SAP.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="d7a0f-140">Hola tooestablish vincular relación, en la nube de objeto de negocios de SAP, para **nombre de usuario**, asignar un valor de Hola de hello **nombre de usuario** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="d7a0f-141">tooconfigure y prueba de inicio de sesión único en Azure AD con SAP Business objeto nube, Hola completa después de tareas:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="d7a0f-142">[Configuración del inicio de sesión único de Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="d7a0f-143">Configura un toouse de usuario de esta característica.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="d7a0f-144">[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="d7a0f-145">Pruebas AD Azure inicio de sesión único con usuario hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="d7a0f-146">[Creación de un usuario de prueba de SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="d7a0f-147">Crea a un equivalente de Britta Simon en nube de objeto de negocios de SAP que está vinculado toohello representación de Azure AD del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="d7a0f-148">[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="d7a0f-149">Configura Britta Simon toouse inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7a0f-150">[Prueba de inicio de sesión único](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="d7a0f-151">Comprueba que la configuración de hello funciona.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="d7a0f-152">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a0f-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="d7a0f-153">En esta sección, activar Azure AD único inicio de sesión en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="d7a0f-154">A continuación, configura el inicio de sesión único en la aplicación SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="d7a0f-155">tooset de inicio de sesión único en Azure AD con SAP Business objeto nube:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="d7a0f-156">En el portal de Azure, en Hola Hola **SAP Business objeto nube** página de integración de aplicaciones, seleccione **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Seleccionar Inicio de sesión único][4]

2. <span data-ttu-id="d7a0f-158">En hello **inicio de sesión único** página, para **modo**, seleccione **sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Seleccionar Inicio de sesión basado en SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="d7a0f-160">En **dominio de nube de objeto de negocio de SAP y las direcciones URL**completa Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="d7a0f-161">Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL con hello siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="d7a0f-162">Hola **identificador** cuadro, escriba una dirección URL con hello siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Direcciones URL de la página Dominio y direcciones URL de SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="d7a0f-164">los valores de Hello en estas direcciones URL son únicamente como demostración.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="d7a0f-165">Actualizar valores de hello con hello real sesión dirección URL y el identificador de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="d7a0f-166">tooget Hola inicio de sesión dirección URL, póngase en contacto con hello [equipo de soporte técnico de SAP Business objeto nube Client](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="d7a0f-167">Puede obtener la dirección URL de identificación de hello mediante la descarga de metadatos de la nube de objeto de negocios de SAP Hola desde la consola de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="d7a0f-168">Esto se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="d7a0f-169">En **Certificado de firma de SAML**, seleccione **XML de metadatos**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="d7a0f-170">A continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-170">Then, save hello metadata file on your computer.</span></span>

    ![Seleccionar XML de metadatos](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="d7a0f-172">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-172">Select **Save**.</span></span>

    ![Seleccionar Guardar](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d7a0f-174">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de SAP Business objeto nube tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="d7a0f-175">Seleccione **Menu** > **System** > **Administration** (Menú > Sistema > Administración).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Seleccionar Menu (Menú), System (Sistema) y, luego, Administration (Administración)](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="d7a0f-177">En hello **seguridad** ficha, seleccione hello **editar** el icono de (lápiz PC).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![En la pestaña de seguridad de hello, seleccione el icono de edición de Hola](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="d7a0f-179">Como **Authentication Method** (Método de autenticación), seleccione **SAML Single Sign-On (SSO)** (Inicio de sesión único [SSO] de SAML).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Seleccione SAML Single Sign-On para el método de autenticación de Hola](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="d7a0f-181">toodownload Hola proveedor metadatos del servicio (paso 1), seleccione **descargar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="d7a0f-182">En el archivo de metadatos de hello, busque y copie hello **entityID** valor.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="d7a0f-183">Hola Azure portal, en **dominio de nube de objeto de negocio de SAP y las direcciones URL**, pegue el valor de Hola Hola **identificador** cuadro.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Copie y pegue el valor entityID de Hola](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="d7a0f-185">tooupload Hola proveedor metadatos del servicio (paso 2) en el archivo hello que descargó desde Hola portal de Azure, en **metadatos cargar el proveedor de identidades**, seleccione **cargar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![En Upload Identity Provider metadata (Cargar metadatos del proveedor de identidades), seleccionar Upload (Cargar)](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="d7a0f-187">Hola **usuario atributo** lista, los atributos de usuario de hello seleccione (paso 3) que desea toouse para su implementación.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="d7a0f-188">Este atributo de usuario asigna toohello proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="d7a0f-189">un atributo personalizado en la página del usuario de hello, use hello tooenter **personalizado SAML asignación** opción.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="d7a0f-190">O bien, puede seleccionar **correo electrónico** o **Id. de usuario** como atributo de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="d7a0f-191">En nuestro ejemplo, hemos seleccionado **correo electrónico** porque asignamos Hola notificación de identificador de usuario con hello **userprincipalname** atributo Hola **atributos de usuario** sección Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="d7a0f-192">Esto proporciona un correo electrónico de usuario único, que se envía toohello aplicación en la nube de objeto de negocios de SAP en cada respuesta SAML correcta.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Seleccionar Atributos de usuario](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="d7a0f-194">cuenta de hello tooverify con el proveedor de identidades de hello (paso 4), en hello **credenciales de inicio de sesión (correo electrónico)** cuadro, escriba la dirección de correo electrónico del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="d7a0f-195">A continuación, seleccione **Verify Account** (Comprobar cuenta).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="d7a0f-196">sistema de Hello agrega la cuenta de usuario de las credenciales de inicio de sesión toohello.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![Escribir Email (Correo electrónico) y seleccionar Verify Account (Comprobar cuenta)](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="d7a0f-198">Seleccione hello **guardar** icono.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-198">Select hello **Save** icon.</span></span>

    ![Icono Save (Guardar)](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="d7a0f-200">Puede leer una versión concisa de estas instrucciones en hello [portal de Azure](https://portal.azure.com), mientras que va a configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="d7a0f-201">Después de agregar la aplicación hello seleccionando **Active Directory** > **aplicaciones empresariales**, seleccione hello **Single Sign-On** ficha. Puede tener acceso a la documentación de hello incrustado en hello **configuración** sección final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="d7a0f-202">Para más información, consulte la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d7a0f-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a0f-203">Create an Azure AD test user</span></span>
<span data-ttu-id="d7a0f-204">En esta sección, creará un usuario de prueba denominado a Britta Simon Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="d7a0f-205">toocreate un usuario de prueba en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="d7a0f-206">En el portal de Azure, en el menú de la izquierda, Hola Hola seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7a0f-208">lista de hello toodisplay de usuarios, seleccionados **usuarios y grupos**y, a continuación, seleccione **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7a0f-210">Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7a0f-212">Hola **usuario** cuadro de diálogo, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="d7a0f-213">Hola **nombre** cuadro, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="d7a0f-214">Hola **nombre de usuario** cuadro, escriba la dirección de correo electrónico de saludo del usuario de hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="d7a0f-215">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="d7a0f-216">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-216">Select **Create**.</span></span>

        ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Creación de un usuario de Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="d7a0f-219">Creación de un usuario de prueba de SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="d7a0f-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="d7a0f-220">Usuarios de Azure AD deben estar aprovisionados en la nube de objeto de negocios de SAP antes de poder iniciar sesión tooSAP nube del objeto de negocios.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="d7a0f-221">En SAP Business Object Cloud, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="d7a0f-222">tooprovision una cuenta de usuario:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="d7a0f-223">Inicie sesión en tooyour sitio SAP Business objeto nube de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="d7a0f-224">Seleccione **Menu** > **Security** > **Users** (Menú > Seguridad > Usuarios).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="d7a0f-226">En hello **usuarios** , tooadd nuevos detalles del usuario, seleccione  **+** .</span><span class="sxs-lookup"><span data-stu-id="d7a0f-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Página Add Users (Agregar usuarios)](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="d7a0f-228">A continuación, complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="d7a0f-229">Hola **Id. de usuario** cuadro, escriba Hola identificador de usuario de hello, como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="d7a0f-230">Hola **nombre** cuadro, escriba Hola nombre de usuario de hello, como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="d7a0f-231">Hola **LAST NAME** cuadro, escriba el apellido del nombre de usuario de hello, hello como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="d7a0f-232">Hola **nombre para mostrar** cuadro, escriba el nombre completo de saludo del usuario de hello, como **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="d7a0f-233">Hola **correo electrónico** cuadro, escriba la dirección de correo electrónico de saludo del usuario de hello, como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d7a0f-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="d7a0f-234">En hello **seleccionar Roles de** , seleccione el rol adecuado de hello para el usuario de hello y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Seleccionar rol](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="d7a0f-236">Seleccione hello **guardar** icono.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d7a0f-237">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a0f-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d7a0f-238">En esta sección, que permita que a Hola usuario Britta Simon toouse Azure AD inicio de sesión único mediante la concesión de hello usuario cuenta acceso tooSAP nube del objeto de negocios.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="d7a0f-239">tooassign Britta Simon tooSAP nube del objeto de negocios:</span><span class="sxs-lookup"><span data-stu-id="d7a0f-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="d7a0f-240">Hola portal de Azure, abrir vista de aplicaciones de hello y, haga clic en la vista de directorio toohello.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="d7a0f-241">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d7a0f-243">En la lista de aplicaciones de hello, seleccione **SAP Business objeto nube**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="d7a0f-245">En el menú de la izquierda hello, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-245">In hello left menu, select **Users and groups**.</span></span>

    ![Seleccionar Usuarios y grupos][202] 

4. <span data-ttu-id="d7a0f-247">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-247">Select **Add**.</span></span> <span data-ttu-id="d7a0f-248">A continuación, en hello **Agregar asignación** página, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![página Agregar asignación de Hola][203]

5. <span data-ttu-id="d7a0f-250">En hello **usuarios y grupos** página, en la lista de Hola de usuarios, seleccionados **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="d7a0f-251">En hello **usuarios y grupos** página, seleccione **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="d7a0f-252">En hello **Agregar asignación** página, seleccione **asignar**.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Asigne el rol de usuario de Hola][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d7a0f-254">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d7a0f-254">Test single sign-on</span></span>

<span data-ttu-id="d7a0f-255">En esta sección, probará la configuración de inicio de sesión única de Azure AD mediante el panel de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="d7a0f-256">Cuando se selecciona mosaico de nube de objeto de negocios de SAP de hello en el panel de acceso hello, se debe sesión automáticamente en tooyour aplicación en la nube de objeto de negocios de SAP.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="d7a0f-257">Para obtener más información acerca del panel de acceso de hello, consulte [panel de acceso de introducción toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7a0f-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d7a0f-258">Additional resources</span></span>

* [<span data-ttu-id="d7a0f-259">Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7a0f-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7a0f-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7a0f-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

