---
title: "Tutorial: Integración de Azure Active Directory con OfficeSpace Software | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="2ea1d-103">Tutorial: Integración de Azure Active Directory con OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="2ea1d-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="2ea1d-104">En este tutorial, aprenderá cómo toointegrate OfficeSpace Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ea1d-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ea1d-105">Integración de OfficeSpace Software con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ea1d-106">Puede controlar en Azure AD que tenga acceso tooOfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="2ea1d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooOfficeSpace Software (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2ea1d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2ea1d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ea1d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ea1d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2ea1d-110">Prerequisites</span></span>

<span data-ttu-id="2ea1d-111">tooconfigure integración de Azure AD con OfficeSpace Software, necesitará Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="2ea1d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ea1d-113">Un suscripción habilitada para el inicio de sesión único en OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="2ea1d-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ea1d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ea1d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ea1d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ea1d-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ea1d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ea1d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2ea1d-118">Scenario description</span></span>
<span data-ttu-id="2ea1d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ea1d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ea1d-121">Agregar OfficeSpace Software desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2ea1d-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="2ea1d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea1d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="2ea1d-123">Agregar OfficeSpace Software desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2ea1d-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="2ea1d-124">integración de hello tooconfigure de OfficeSpace Software en Azure AD, deberá tooadd OfficeSpace Software de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ea1d-125">**tooadd OfficeSpace Software desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ea1d-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ea1d-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="2ea1d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ea1d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="2ea1d-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="2ea1d-133">En el cuadro de búsqueda de hello, escriba **OfficeSpace Software**, seleccione **OfficeSpace Software** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de OfficeSpace Software Hola](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2ea1d-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea1d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2ea1d-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con OfficeSpace Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2ea1d-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ea1d-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en OfficeSpace Software es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="2ea1d-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en OfficeSpace Software necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="2ea1d-139">En OfficeSpace Software, asignar el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ea1d-140">tooconfigure y prueba de inicio de sesión único en Azure AD con OfficeSpace Software, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ea1d-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ea1d-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ea1d-143">**[Crear un usuario de prueba de OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave un equivalente de Britta Simon en OfficeSpace Software que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ea1d-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ea1d-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2ea1d-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea1d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2ea1d-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="2ea1d-148">**inicio de sesión único en tooconfigure Azure AD con OfficeSpace Software, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ea1d-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ea1d-149">En el portal de Azure, en Hola Hola **OfficeSpace Software** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="2ea1d-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="2ea1d-153">En hello **OfficeSpace Software dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="2ea1d-155">a.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-155">a.</span></span> <span data-ttu-id="2ea1d-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="2ea1d-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="2ea1d-157">b.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-157">b.</span></span> <span data-ttu-id="2ea1d-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="2ea1d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ea1d-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-159">These values are not real.</span></span> <span data-ttu-id="2ea1d-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2ea1d-161">Póngase en contacto con [equipo de soporte técnico de OfficeSpace Software cliente](mailto:support@officespacesoftware.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="2ea1d-162">Aplicación de OfficeSpace Software espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="2ea1d-163">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="2ea1d-164">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2ea1d-165">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-165">hello following screenshot shows an example for this.</span></span>
    
    ![Configuración del atributo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="2ea1d-167">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, seleccione **user.mail** como **identificador de usuario** y para cada fila se muestra en la tabla de Hola a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="2ea1d-168">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="2ea1d-168">Attribute Name</span></span> | <span data-ttu-id="2ea1d-169">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="2ea1d-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="2ea1d-170">email</span><span class="sxs-lookup"><span data-stu-id="2ea1d-170">email</span></span> | <span data-ttu-id="2ea1d-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="2ea1d-171">user.mail</span></span> |
    | <span data-ttu-id="2ea1d-172">name</span><span class="sxs-lookup"><span data-stu-id="2ea1d-172">name</span></span> | <span data-ttu-id="2ea1d-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="2ea1d-173">user.displayname</span></span> |
    | <span data-ttu-id="2ea1d-174">first_name</span><span class="sxs-lookup"><span data-stu-id="2ea1d-174">first_name</span></span> | <span data-ttu-id="2ea1d-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="2ea1d-175">user.givenname</span></span> |
    | <span data-ttu-id="2ea1d-176">last_name</span><span class="sxs-lookup"><span data-stu-id="2ea1d-176">last_name</span></span> | <span data-ttu-id="2ea1d-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="2ea1d-177">user.surname</span></span> |

    <span data-ttu-id="2ea1d-178">a.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-178">a.</span></span> <span data-ttu-id="2ea1d-179">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="2ea1d-180">Configuración de la agregación</span><span class="sxs-lookup"><span data-stu-id="2ea1d-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configuración del atributo](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="2ea1d-182">b.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-182">b.</span></span> <span data-ttu-id="2ea1d-183">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="2ea1d-184">c.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-184">c.</span></span> <span data-ttu-id="2ea1d-185">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="2ea1d-186">d.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-186">d.</span></span> <span data-ttu-id="2ea1d-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="2ea1d-188">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="2ea1d-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2ea1d-190">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2ea1d-192">En hello **OfficeSpace Software configuración** sección, haga clic en **configurar OfficeSpace Software** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ea1d-193">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="2ea1d-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="2ea1d-195">En otra ventana del explorador web, inicie sesión en como administrador en el inquilino de OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="2ea1d-196">Vaya demasiado**configuración** y haga clic en **conectores**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-196">Go too**Settings** and click **Connectors**.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="2ea1d-198">Haga clic en **Autenticación SAML**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-198">Click **SAML Authentication**.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="2ea1d-200">Hola **autenticación SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="2ea1d-202">a.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-202">a.</span></span> <span data-ttu-id="2ea1d-203">Hola **dirección url del proveedor de cierre de sesión** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ea1d-204">b.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-204">b.</span></span> <span data-ttu-id="2ea1d-205">Hola **dirección url de destino de idp de cliente** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ea1d-206">c.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-206">c.</span></span> <span data-ttu-id="2ea1d-207">Hola pegar **huella digital** valor que ha copiado desde el portal de Azure, en hello **huella digital de certificado de cliente IDP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="2ea1d-208">d.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-208">d.</span></span> <span data-ttu-id="2ea1d-209">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="2ea1d-210">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="2ea1d-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ea1d-211">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ea1d-212">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ea1d-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2ea1d-213">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea1d-213">Create an Azure AD test user</span></span>

<span data-ttu-id="2ea1d-214">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="2ea1d-216">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ea1d-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ea1d-217">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2ea1d-219">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2ea1d-221">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2ea1d-223">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ea1d-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2ea1d-225">a.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-225">a.</span></span> <span data-ttu-id="2ea1d-226">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ea1d-227">b.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-227">b.</span></span> <span data-ttu-id="2ea1d-228">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2ea1d-229">c.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-229">c.</span></span> <span data-ttu-id="2ea1d-230">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2ea1d-231">d.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-231">d.</span></span> <span data-ttu-id="2ea1d-232">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="2ea1d-233">Creación de un usuario de prueba de OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="2ea1d-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="2ea1d-234">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="2ea1d-235">OfficeSpace Software admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="2ea1d-236">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-236">There is no action item for you in this section.</span></span> <span data-ttu-id="2ea1d-237">Si no existe todavía, se creará un nuevo usuario durante una tooaccess de intento de OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea1d-238">Si necesita un usuario toocreate manualmente, necesita tooContact [equipo de soporte técnico de OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="2ea1d-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2ea1d-239">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea1d-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2ea1d-240">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooOfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="2ea1d-242">**tooassign Britta Simon tooOfficeSpace Software, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ea1d-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ea1d-243">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2ea1d-245">En la lista de aplicaciones de hello, seleccione **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![vínculo de OfficeSpace Software en la lista de aplicaciones de Hola Hola](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="2ea1d-247">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="2ea1d-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-249">Click **Add** button.</span></span> <span data-ttu-id="2ea1d-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="2ea1d-252">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ea1d-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ea1d-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2ea1d-255">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="2ea1d-255">Test single sign-on</span></span>

<span data-ttu-id="2ea1d-256">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ea1d-257">Al hacer clic en hello OfficeSpace Software disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="2ea1d-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ea1d-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2ea1d-258">Additional resources</span></span>

* [<span data-ttu-id="2ea1d-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ea1d-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ea1d-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ea1d-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

