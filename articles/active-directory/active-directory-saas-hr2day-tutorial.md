---
title: "Tutorial: integración de Azure Active Directory con HR2day by Merces | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y HR2day por Merces."
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
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="e925a-103">Tutorial: Integración de Azure Active Directory con HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="e925a-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="e925a-104">En este tutorial, aprenderá cómo toointegrate HR2day por Merces con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e925a-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e925a-105">Integración HR2day por Merces con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e925a-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e925a-106">Puede controlar en Azure AD que tenga acceso tooHR2day por Merces.</span><span class="sxs-lookup"><span data-stu-id="e925a-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="e925a-107">Puede permitir a los usuarios tooautomatically obtener inicia sesión en tooHR2day Merces con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e925a-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="e925a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e925a-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="e925a-109">Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e925a-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e925a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e925a-110">Prerequisites</span></span>

<span data-ttu-id="e925a-111">integración de Azure AD con HR2day por Merces tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e925a-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="e925a-112">Una suscripción de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e925a-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="e925a-113">Una suscripción habilitada para el inicio de sesión único en HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="e925a-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e925a-114">No se recomienda usar un Hola de tootest del entorno de producción de los pasos en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e925a-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="e925a-115">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e925a-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="e925a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e925a-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="e925a-117">Puede obtener [un versión de evaluación gratuita de un mes de Azure AD](https://azure.microsoft.com/pricing/free-trial/) si aún no la tiene.</span><span class="sxs-lookup"><span data-stu-id="e925a-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="e925a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e925a-118">Scenario description</span></span>
<span data-ttu-id="e925a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e925a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e925a-120">escenario de Hola que se detallan en este documento consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e925a-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="e925a-121">Agregar HR2day por Merces desde la Galería de Hola.</span><span class="sxs-lookup"><span data-stu-id="e925a-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="e925a-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e925a-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="e925a-123">Agregar HR2day por Merces de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e925a-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="e925a-124">integración de hello tooconfigure de HR2day por Merces en Azure AD, agregue HR2day por Merces de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e925a-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e925a-125">**tooadd HR2day por Merces de galería de hello, tomar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e925a-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="e925a-126">Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, seleccione hello **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e925a-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e925a-128">Vaya demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e925a-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="e925a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e925a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e925a-131">tooadd una nueva aplicación, seleccione hello **nueva aplicación** botón en la parte superior de Hola Hola del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e925a-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e925a-133">En el cuadro de búsqueda de hello, escriba **HR2day por Merces**.</span><span class="sxs-lookup"><span data-stu-id="e925a-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="e925a-135">En el panel de resultados de hello, seleccione **HR2day por Merces**y, a continuación, seleccione hello **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e925a-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e925a-137">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="e925a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e925a-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con HR2day by Merces con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e925a-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e925a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow quién Hola homólogo usuario en HR2day por Merces tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e925a-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="e925a-140">En otras palabras, necesita tooestablish un vínculo entre un usuario de Azure AD y el usuario relacionado de hello en HR2day por Merces.</span><span class="sxs-lookup"><span data-stu-id="e925a-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="e925a-141">En HR2day por Merces, asigne hello **nombre de usuario** en Azure AD demasiado **nombre de usuario** relación de hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="e925a-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="e925a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con HR2day por Merces, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e925a-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e925a-143">[Configurar inicio de sesión único en Azure AD](#configuring-azure-ad-single-sign-on): habilitar el toouse de los usuarios de esta característica.</span><span class="sxs-lookup"><span data-stu-id="e925a-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="e925a-144">[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user): pruebe el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e925a-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e925a-145">[Crear un HR2day por usuario de prueba de Merces](#creating-an-hr2day-by-merces-test-user): crear un equivalente de Britta Simon en HR2day por Merces que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="e925a-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e925a-146">[Asignar el usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user): habilitar Britta Simon toouse inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e925a-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e925a-147">[Probar el inicio de sesión único](#testing-single-sign-on): comprobar si la configuración de hello funciona.</span><span class="sxs-lookup"><span data-stu-id="e925a-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e925a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e925a-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e925a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su HR2day Merces aplicación.</span><span class="sxs-lookup"><span data-stu-id="e925a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="e925a-150">**inicio de sesión único en Azure AD tooconfigure con HR2day por Merces, tomar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e925a-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="e925a-151">En el portal de Azure, en Hola Hola **HR2day por Merces** página de integración de aplicaciones, seleccione **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e925a-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e925a-153">tooenable inicio de sesión único, Hola **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="e925a-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="e925a-155">Hola **HR2day Merces dominio y las direcciones URL** sección, llevar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e925a-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="e925a-157">a.</span><span class="sxs-lookup"><span data-stu-id="e925a-157">a.</span></span> <span data-ttu-id="e925a-158">Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL mediante el uso de hello siguiente patrón: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="e925a-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="e925a-159">b.</span><span class="sxs-lookup"><span data-stu-id="e925a-159">b.</span></span> <span data-ttu-id="e925a-160">Hola **identificador** cuadro, escriba una dirección URL mediante el uso de hello siguiente patrón: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="e925a-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e925a-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e925a-161">These values are not real.</span></span> <span data-ttu-id="e925a-162">Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador.</span><span class="sxs-lookup"><span data-stu-id="e925a-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="e925a-163">Póngase en contacto con hello [HR2day equipo de soporte técnico de cliente de Merces](mailto:servicedesk@merces.nl) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="e925a-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="e925a-164">En hello **el certificado de firma de SAML** sección, seleccione **Certificate(Base64)**y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e925a-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="e925a-166">Esta sección se describe cómo tooenable usuarios tooauthenticate tooHR2day por Merces con su cuenta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e925a-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="e925a-167">Para hacerlo mediante el uso de federación que se basa en hello protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="e925a-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="e925a-168">Su HR2day Merces aplicación espera las aserciones de SAML de hello en un formato específico, que requiere el token SAML de tooyour de asignaciones de atributo personalizado de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e925a-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="e925a-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="e925a-169">hello following screenshot shows an example of this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="e925a-171">Para poder configurar la aserción de SAML de hello, debe ponerse en contacto con hello [HR2day equipo de soporte técnico de Merces cliente](mailto:servicedesk@merces.nl) y solicite el valor de Hola de atributo del identificador único de hello para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="e925a-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="e925a-172">Necesita esta valor toocomplete Hola se analiza en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e925a-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="e925a-173">Hola **inicio de sesión único** cuadro de diálogo hello **atributos de usuario** sección, configure el atributo de token de SAML de hello como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="e925a-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="e925a-174">A continuación, tomar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="e925a-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="e925a-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="e925a-175">Attribute name</span></span>    |   <span data-ttu-id="e925a-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="e925a-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="e925a-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="e925a-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="e925a-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="e925a-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="e925a-179">a.</span><span class="sxs-lookup"><span data-stu-id="e925a-179">a.</span></span> <span data-ttu-id="e925a-180">Hola tooopen **Agregar atributo** cuadro de diálogo, seleccione **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="e925a-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e925a-183">b.</span><span class="sxs-lookup"><span data-stu-id="e925a-183">b.</span></span> <span data-ttu-id="e925a-184">Hola **nombre** , escriba **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="e925a-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="e925a-185">c.</span><span class="sxs-lookup"><span data-stu-id="e925a-185">c.</span></span> <span data-ttu-id="e925a-186">De hello **valor** lista, seleccione **Join()**.</span><span class="sxs-lookup"><span data-stu-id="e925a-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="e925a-187">d.</span><span class="sxs-lookup"><span data-stu-id="e925a-187">d.</span></span> <span data-ttu-id="e925a-188">De hello **String1** lista, seleccione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="e925a-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="e925a-189">e.</span><span class="sxs-lookup"><span data-stu-id="e925a-189">e.</span></span> <span data-ttu-id="e925a-190">Para **String2**, escriba Hola identificador único proporcionado por el equipo de HR2day.</span><span class="sxs-lookup"><span data-stu-id="e925a-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="e925a-191">f.</span><span class="sxs-lookup"><span data-stu-id="e925a-191">f.</span></span> <span data-ttu-id="e925a-192">Hola **separador** , escriba  **@** .</span><span class="sxs-lookup"><span data-stu-id="e925a-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="e925a-193">g.</span><span class="sxs-lookup"><span data-stu-id="e925a-193">g.</span></span> <span data-ttu-id="e925a-194">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e925a-194">Select **Ok**.</span></span>

7. <span data-ttu-id="e925a-195">Seleccione hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="e925a-195">Select hello **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e925a-197">Hola **HR2day por la configuración de Merces** sección, seleccione **HR2day configurar por Merces** tooopen hello **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="e925a-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="e925a-198">Hola copia **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML Single Sign-On dirección URL del servicio** de hello **referencia rápida** sección.</span><span class="sxs-lookup"><span data-stu-id="e925a-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="e925a-200">tooconfigure SSO para su aplicación, póngase en contacto con hello [HR2day Merces equipo de soporte técnico de cliente](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="e925a-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="e925a-201">Adjuntar Hola descargado **Certificate(Base64)** correo electrónico tooyour de archivos.</span><span class="sxs-lookup"><span data-stu-id="e925a-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="e925a-202">También proporcionan hello **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML Single Sign-On dirección URL del servicio** para que se pueden configurar para la integración de SSO.</span><span class="sxs-lookup"><span data-stu-id="e925a-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="e925a-203">Indique el equipo de Merces toohello que esta integración debe Hola toobe de Id. de entidad establecida con el patrón de hello **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="e925a-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="e925a-204">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e925a-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e925a-205">Después de agregar esta aplicación de hello **Active Directory** > **aplicaciones empresariales** sección, seleccione hello **Single Sign-On** ficha. Hola acceso incrusta documentación a través de hello **configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e925a-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e925a-206">Puede leer más acerca de la característica de documentación de embedded Hola Hola [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e925a-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e925a-207">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e925a-207">Create an Azure AD test user</span></span>
<span data-ttu-id="e925a-208">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e925a-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e925a-210">**toocreate un usuario de prueba en Azure AD, tomar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e925a-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="e925a-211">Hola **portal de Azure**, en Hola panel de navegación izquierdo, seleccione hello **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e925a-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e925a-213">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, seleccione **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e925a-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e925a-215">Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar** en la parte superior de Hola Hola del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e925a-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e925a-217">Hola **usuario** cuadro de diálogo, Hola toman pasos:</span><span class="sxs-lookup"><span data-stu-id="e925a-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e925a-219">a.</span><span class="sxs-lookup"><span data-stu-id="e925a-219">a.</span></span> <span data-ttu-id="e925a-220">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e925a-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e925a-221">b.</span><span class="sxs-lookup"><span data-stu-id="e925a-221">b.</span></span> <span data-ttu-id="e925a-222">Hola **nombre de usuario** cuadro, Hola de tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e925a-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e925a-223">c.</span><span class="sxs-lookup"><span data-stu-id="e925a-223">c.</span></span> <span data-ttu-id="e925a-224">Seleccione **Mostrar contraseña**a continuación, anote la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="e925a-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="e925a-225">d.</span><span class="sxs-lookup"><span data-stu-id="e925a-225">d.</span></span> <span data-ttu-id="e925a-226">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e925a-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="e925a-227">Creación de un usuario de prueba de HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="e925a-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="e925a-228">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en HR2day Merces toocreate.</span><span class="sxs-lookup"><span data-stu-id="e925a-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="e925a-229">los usuarios de hello tooadd en la cuenta de hello HR2day, trabajar con hello [HR2day Merces equipo de soporte técnico de cliente](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="e925a-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="e925a-230">Si necesita un usuario toocreate manualmente, póngase en contacto con hello [HR2day Merces equipo de soporte técnico de cliente](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="e925a-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e925a-231">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e925a-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e925a-232">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooHR2day acceso por Merces.</span><span class="sxs-lookup"><span data-stu-id="e925a-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e925a-234">**tooassign Britta Simon tooHR2day por Merces, tome Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e925a-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="e925a-235">Hola Azure ver aplicaciones de portal, abra Hola, vaya toohello vista del directorio y, a continuación, vaya demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e925a-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="e925a-236">A continuación, seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e925a-236">Next, select **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e925a-238">En la lista de aplicaciones de hello, seleccione **HR2day por Merces**.</span><span class="sxs-lookup"><span data-stu-id="e925a-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="e925a-240">En el menú de Hola Hola izquierda, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e925a-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e925a-242">Seleccione hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="e925a-242">Select hello **Add** button.</span></span> <span data-ttu-id="e925a-243">A continuación, en hello **Agregar asignación** cuadro de diálogo, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e925a-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e925a-245">Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e925a-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="e925a-246">Haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="e925a-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="e925a-247">Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.</span><span class="sxs-lookup"><span data-stu-id="e925a-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e925a-248">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e925a-248">Test single sign-on</span></span>

<span data-ttu-id="e925a-249">Hola objetivo de esta sección es tootest su único inicio de sesión en configuración de Azure AD mediante el uso de Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e925a-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="e925a-250">Al seleccionar hello HR2day Merces icono en el Panel de acceso de hello, que automáticamente obtener iniciado sesión en tooyour HR2day Merces aplicación.</span><span class="sxs-lookup"><span data-stu-id="e925a-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e925a-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e925a-251">Additional resources</span></span>

* [<span data-ttu-id="e925a-252">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e925a-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e925a-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e925a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

