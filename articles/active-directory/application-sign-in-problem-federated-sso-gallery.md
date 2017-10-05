---
title: "Problemas al iniciar sesión en una aplicación de la galería configurada para inicio de sesión único federado | Microsoft Docs"
description: "Instrucciones para resolver errores específicos al iniciar sesión en una aplicación que se ha configurado para un inicio de sesión único federado basado en SAML con Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0fc5a8eb3d033d60bf6082d61bf1698924ab91c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="0ef62-103">Problemas al iniciar sesión en una aplicación de la galería configurada para inicio de sesión único federado</span><span class="sxs-lookup"><span data-stu-id="0ef62-103">Problems signing in to a gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="0ef62-104">Para solucionar el problema, debe comprobar la configuración de la aplicación en Azure AD de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ef62-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="0ef62-105">Ha seguido todos los pasos de configuración de la aplicación de la galería de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef62-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="0ef62-106">El identificador y la dirección URL de respuesta configurados en AAD coinciden con los valores previstos en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="0ef62-107">Ha asignado usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="0ef62-108">No se encontró la aplicación en el directorio</span><span class="sxs-lookup"><span data-stu-id="0ef62-108">Application not found in directory</span></span>

<span data-ttu-id="0ef62-109">*Error AADSTS70001: No se encontró la aplicación con el identificador "https://contoso.com" en el directorio*.</span><span class="sxs-lookup"><span data-stu-id="0ef62-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="0ef62-110">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="0ef62-110">**Possible cause**</span></span>

<span data-ttu-id="0ef62-111">El atributo Issuer que se envía de la aplicación a Azure AD en la solicitud SAML no coincide con el valor de identificador configurado en la aplicación Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef62-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="0ef62-112">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="0ef62-112">**Resolution**</span></span>

<span data-ttu-id="0ef62-113">Asegúrese de que el atributo Issuer de la solicitud SAML coincide con el valor del identificador configurado en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0ef62-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="0ef62-114">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ef62-115">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="0ef62-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ef62-116">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ef62-117">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ef62-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ef62-118">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0ef62-118">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0ef62-119">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0ef62-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0ef62-120">Seleccionar la aplicación que desea configurar para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0ef62-120">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="0ef62-121">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ef62-122">Vaya a la sección **Dominio y direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-122">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="0ef62-123">Compruebe que el valor del cuadro de texto Identificador coincide con el valor del identificador mostrado en el error.</span><span class="sxs-lookup"><span data-stu-id="0ef62-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="0ef62-124">Después de actualizar el valor del identificador de Azure AD y de comprobar que coincide con el valor enviado por la aplicación en la solicitud SAML, podrá iniciar sesión en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="0ef62-125">La dirección de respuesta no coincide con las direcciones de respuesta configuradas para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-125">The reply address does not match the reply addresses configured for the application.</span></span>

<span data-ttu-id="0ef62-126">*Error AADSTS50011: La dirección de respuesta "https://contoso.com" no coincide con las direcciones de respuesta configuradas para la aplicación*</span><span class="sxs-lookup"><span data-stu-id="0ef62-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span>

<span data-ttu-id="0ef62-127">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="0ef62-127">**Possible cause**</span></span>

<span data-ttu-id="0ef62-128">El valor de AssertionConsumerServiceURL en la solicitud SAML no coincide con el valor o patrón de la dirección URL de respuesta configurada en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef62-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="0ef62-129">El valor de AssertionConsumerServiceURL en la solicitud SAML es la dirección URL que se ve en el error.</span><span class="sxs-lookup"><span data-stu-id="0ef62-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span>

<span data-ttu-id="0ef62-130">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="0ef62-130">**Resolution**</span></span>

<span data-ttu-id="0ef62-131">Asegúrese de que el valor de AssertionConsumerServiceURL en la solicitud SAML coincide con el valor de la dirección URL de respuesta configurada en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef62-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="0ef62-132">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ef62-133">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="0ef62-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ef62-134">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ef62-135">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ef62-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ef62-136">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0ef62-136">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0ef62-137">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0ef62-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0ef62-138">Seleccionar la aplicación que desea configurar para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0ef62-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="0ef62-139">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ef62-140">Vaya a la sección **Dominio y direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="0ef62-141">Compruebe o actualice el valor en el cuadro de texto Dirección URL de respuesta para que coincida con el valor de AssertionConsumerServiceURL en la solicitud SAML.</span><span class="sxs-lookup"><span data-stu-id="0ef62-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>  
    * <span data-ttu-id="0ef62-142">Si no ve el cuadro de texto Dirección URL de respuesta, active la casilla **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="0ef62-143">Después de actualizar el valor de la dirección URL de respuesta en Azure AD y de comprobar que coincide con el valor enviado por la aplicación en la solicitud SAML, podrá iniciar sesión en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="0ef62-144">Usuario no asignado a un rol</span><span class="sxs-lookup"><span data-stu-id="0ef62-144">User not assigned a role</span></span>

<span data-ttu-id="0ef62-145">*Error AADSTS50105: El usuario con sesión iniciada "brian@contoso.com" no está asignado a un rol de la aplicación*.</span><span class="sxs-lookup"><span data-stu-id="0ef62-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span></span>

<span data-ttu-id="0ef62-146">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="0ef62-146">**Possible cause**</span></span>

<span data-ttu-id="0ef62-147">El usuario no tiene acceso a la aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef62-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="0ef62-148">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="0ef62-148">**Resolution**</span></span>

<span data-ttu-id="0ef62-149">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0ef62-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="0ef62-150">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0ef62-151">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="0ef62-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ef62-152">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ef62-153">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ef62-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ef62-154">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0ef62-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0ef62-155">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0ef62-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0ef62-156">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="0ef62-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="0ef62-157">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ef62-158">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="0ef62-159">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="0ef62-160">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="0ef62-161">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="0ef62-162">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="0ef62-163">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="0ef62-164">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="0ef62-165">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="0ef62-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="0ef62-166">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="0ef62-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="0ef62-167">Tras un breve período de tiempo, los usuarios seleccionados podrán iniciar estas aplicaciones mediante los métodos descritos en la sección de descripción de la solución.</span><span class="sxs-lookup"><span data-stu-id="0ef62-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="0ef62-168">No es una solicitud SAML válida</span><span class="sxs-lookup"><span data-stu-id="0ef62-168">Not a valid SAML Request</span></span>

<span data-ttu-id="0ef62-169">*Error AADSTS75005: La solicitud no es un mensaje de protocolo Saml2 válido.*</span><span class="sxs-lookup"><span data-stu-id="0ef62-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="0ef62-170">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="0ef62-170">**Possible cause**</span></span>

<span data-ttu-id="0ef62-171">Azure AD no admite la solicitud SAML enviada por la aplicación para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0ef62-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="0ef62-172">Algunos de los problemas más comunes son:</span><span class="sxs-lookup"><span data-stu-id="0ef62-172">Some common issues are:</span></span>

-   <span data-ttu-id="0ef62-173">Faltan campos obligatorios en la solicitud SAML</span><span class="sxs-lookup"><span data-stu-id="0ef62-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="0ef62-174">Método codificado de la solicitud SAML</span><span class="sxs-lookup"><span data-stu-id="0ef62-174">SAML request encoded method</span></span>

<span data-ttu-id="0ef62-175">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="0ef62-175">**Resolution**</span></span>

1.  <span data-ttu-id="0ef62-176">Capture la solicitud SAML.</span><span class="sxs-lookup"><span data-stu-id="0ef62-176">Capture SAML request.</span></span> <span data-ttu-id="0ef62-177">Siga el tutorial de [Cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) para obtener información sobre cómo capturar la solicitud SAML.</span><span class="sxs-lookup"><span data-stu-id="0ef62-177">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="0ef62-178">Póngase en contacto con el proveedor de la aplicación y comparta:</span><span class="sxs-lookup"><span data-stu-id="0ef62-178">Contact the application vendor and share:</span></span>

   -   <span data-ttu-id="0ef62-179">La solicitud SAML</span><span class="sxs-lookup"><span data-stu-id="0ef62-179">SAML request</span></span>

   -   [<span data-ttu-id="0ef62-180">Los requisitos del protocolo SAML de inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ef62-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="0ef62-181">Deben validar que admiten la implementación de SAML de Azure AD para inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0ef62-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="0ef62-182">Ningún recurso en la lista requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="0ef62-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="0ef62-183">*Error AADSTS65005: La aplicación cliente ha solicitado el acceso al recurso "00000002-0000-0000-c000-000000000000". Se produjo un error en esta solicitud porque el cliente no ha especificado este recurso en su lista requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="0ef62-183">*Error AADSTS65005:The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="0ef62-184">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="0ef62-184">**Possible cause**</span></span>

<span data-ttu-id="0ef62-185">El objeto de aplicación está dañado.</span><span class="sxs-lookup"><span data-stu-id="0ef62-185">The application object is corrupted.</span></span>

<span data-ttu-id="0ef62-186">**Resolución: opción 1**</span><span class="sxs-lookup"><span data-stu-id="0ef62-186">**Resolution: option 1**</span></span>

<span data-ttu-id="0ef62-187">Para solucionar el problema, agregue el valor de identificador único en la configuración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef62-187">To solve the problem, add the unique Identifier value in the Azure AD configuration.</span></span> <span data-ttu-id="0ef62-188">Para agregar un valor del identificador, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0ef62-188">To add a Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="0ef62-189">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ef62-190">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="0ef62-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ef62-191">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ef62-192">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ef62-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ef62-193">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0ef62-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0ef62-194">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0ef62-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0ef62-195">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0ef62-195">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="0ef62-196">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-196">Once the application loads, click on the **Single sign-on** from the application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="0ef62-197">En la sección **Dominio y dirección URL**, compruebe **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-197">Under the **Domain and URL** section, check on the **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="0ef62-198">En el cuadro de texto **Identificador**, escriba un identificador único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-198">in the **Identifier** textbox type a unique identifier for the application.</span></span>

10. <span data-ttu-id="0ef62-199">**Guarde** la configuración.</span><span class="sxs-lookup"><span data-stu-id="0ef62-199">**Save** the configuration.</span></span>


<span data-ttu-id="0ef62-200">**Resolución: opción 2**</span><span class="sxs-lookup"><span data-stu-id="0ef62-200">**Resolution option 2**</span></span>

<span data-ttu-id="0ef62-201">Si la opción 1 anterior no ha funcionado, pruebe a quitar la aplicación del directorio.</span><span class="sxs-lookup"><span data-stu-id="0ef62-201">If option 1 above did not work for you, try removing the application from the directory.</span></span> <span data-ttu-id="0ef62-202">Después, agregue y vuelva a configurar la aplicación, y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0ef62-202">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="0ef62-203">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-203">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ef62-204">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="0ef62-204">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ef62-205">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-205">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ef62-206">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ef62-206">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ef62-207">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0ef62-207">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0ef62-208">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0ef62-208">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0ef62-209">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0ef62-209">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="0ef62-210">Haga clic en **Eliminar** en la parte superior izquierda de la hoja **Información general** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-210">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="0ef62-211">Actualice Azure AD y agregue la aplicación en la galería de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef62-211">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="0ef62-212">Después, configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-212">Then, Configure the application</span></span>

<span data-ttu-id="0ef62-213"><span id="_Hlk477190176" class="anchor"></span>Tras configurar la aplicación, debe poder iniciar sesión en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="0ef62-214">Certificado o clave no configurados</span><span class="sxs-lookup"><span data-stu-id="0ef62-214">Certificate or key not configured</span></span>

<span data-ttu-id="0ef62-215">*Error AADSTS50003: No hay configurada ninguna clave de firma.*</span><span class="sxs-lookup"><span data-stu-id="0ef62-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="0ef62-216">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="0ef62-216">**Possible cause**</span></span>

<span data-ttu-id="0ef62-217">El objeto de aplicación está dañado y Azure AD no reconoce el certificado configurado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-217">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="0ef62-218">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="0ef62-218">**Resolution**</span></span>

<span data-ttu-id="0ef62-219">Para eliminar y crear un nuevo certificado, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0ef62-219">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="0ef62-220">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-220">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ef62-221">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="0ef62-221">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ef62-222">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-222">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ef62-223">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ef62-223">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ef62-224">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0ef62-224">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="0ef62-225">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0ef62-225">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0ef62-226">Seleccionar la aplicación que desea configurar para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0ef62-226">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="0ef62-227">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ef62-227">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ef62-228">Haga clic en **Crear nuevo certificado** en la sección **Certificado de firma de SAML**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-228">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="0ef62-229">Seleccione la fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="0ef62-229">Select Expiration date.</span></span> <span data-ttu-id="0ef62-230">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="0ef62-231">Active **Activar el certificado nuevo** para reemplazar el certificado activo.</span><span class="sxs-lookup"><span data-stu-id="0ef62-231">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="0ef62-232">Después, haga clic en **Guardar** en la parte superior de la hoja y en Aceptar para activar el certificado de sustitución.</span><span class="sxs-lookup"><span data-stu-id="0ef62-232">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="0ef62-233">En la sección **Certificado de firma de SAML**, haga clic en **Quitar** para quitar el certificado **no usado**.</span><span class="sxs-lookup"><span data-stu-id="0ef62-233">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="0ef62-234">Problema al personalizar las notificaciones SAML que se han enviado a una aplicación</span><span class="sxs-lookup"><span data-stu-id="0ef62-234">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="0ef62-235">Para obtener información sobre cómo personalizar las notificaciones de atributo SAML que se han enviado a su aplicación, vea [Asignación de notificaciones en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping).</span><span class="sxs-lookup"><span data-stu-id="0ef62-235">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ef62-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ef62-236">Next steps</span></span>
[<span data-ttu-id="0ef62-237">Cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ef62-237">How to debug SAML-based single sign-on to applications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
