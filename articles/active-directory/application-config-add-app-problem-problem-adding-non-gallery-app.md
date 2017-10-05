---
title: "Problemas al agregar una aplicación que no pertenece a la galería | Microsoft Docs"
description: "Comprenda los problemas habituales a los que se enfrentan los usuarios al agregar aplicaciones que no pertenecen a la galería"
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
ms.openlocfilehash: bb3fc7877f4e7cafc3904fc67abd87b897874d8a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="cb321-103">Problemas al agregar una aplicación que no pertenece a la galería</span><span class="sxs-lookup"><span data-stu-id="cb321-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="cb321-104">Este artículo le ayuda a conocer los problemas habituales a los que se enfrentan los usuarios al agregar **aplicaciones personalizadas que no pertenecen a la galería** y los pasos que se deben dar para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="cb321-104">This article help you to understand the common problems people face when adding **custom non-gallery applications** and what you can do to resolve them.</span></span> 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="cb321-105">Hice clic en el botón "Agregar" y mi aplicación tardó mucho tiempo en aparecer</span><span class="sxs-lookup"><span data-stu-id="cb321-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="cb321-106">En algunas circunstancias, una aplicación puede tardar entre 1 y 2 minutos (a veces, más) en aparecer después de agregarla a su directorio.</span><span class="sxs-lookup"><span data-stu-id="cb321-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="cb321-107">Aunque este no es el rendimiento normal esperable, puede ver si la incorporación de la aplicación está en curso haciendo clic en el icono de **notificaciones** (la campana) de la esquina superior derecha de [Azure Portal](https://portal.azure.com/) y buscando una notificación **En curso** o **Completado** con la etiqueta **Crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="cb321-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="cb321-108">Si la aplicación nunca se agrega o se produce un error al hacer clic en el botón **Agregar**, verá una **notificación** con un estado de **Error**.</span><span class="sxs-lookup"><span data-stu-id="cb321-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="cb321-109">Si desea obtener más detalles sobre el error para conocer más información o compartirlo con un ingeniero de soporte técnico, puede ver más información sobre el error siguiendo los pasos descritos en [Visualización de los detalles de una notificación del portal](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="cb321-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="cb321-110">Hice clic en el botón "Agregar" y mi aplicación no apareció</span><span class="sxs-lookup"><span data-stu-id="cb321-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="cb321-111">En ocasiones, debido a problemas transitorios, problemas de red o un error, se produce un error al agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb321-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="cb321-112">Puede indicar si esto ocurre si hace clic en el icono de **notificaciones** (la campana) de la esquina superior derecha de Azure Portal y aparece un icono (!) de color rojo junto a la notificación **Crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="cb321-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="cb321-113">Esto indica que se produjo un error al crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb321-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="cb321-114">Si se produce un error al hacer clic en el botón **Agregar**, verá una **notificación** con un estado de **Error**.</span><span class="sxs-lookup"><span data-stu-id="cb321-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="cb321-115">Si desea obtener más detalles sobre el error para conocer más información o compartirlo con un ingeniero de soporte técnico, puede ver más información sobre el error siguiendo los pasos descritos en [Visualización de los detalles de una notificación del portal](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="cb321-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="cb321-116">No sé cómo configurar mi aplicación una vez que la he agregado</span><span class="sxs-lookup"><span data-stu-id="cb321-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="cb321-117">Si necesita ayuda para obtener más detalles sobre las aplicaciones personalizadas, la [biblioteca de documentos de las aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) le ayudará a obtener más información sobre el inicio de sesión único con Azure AD y cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="cb321-117">If you need help learning about custom applications, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="cb321-118">Visualización de los detalles de una notificación del portal</span><span class="sxs-lookup"><span data-stu-id="cb321-118">How to see the details of a portal notification</span></span>

<span data-ttu-id="cb321-119">Puede ver los detalles de cualquier notificación del portal si sigue los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb321-119">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="cb321-120">Haga clic en el icono de **notificaciones** (la campana) de la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cb321-120">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="cb321-121">Seleccione cualquier notificación con un estado de **Error** (aquellas con un icono (!) de color rojo situado junto a ellas).</span><span class="sxs-lookup"><span data-stu-id="cb321-121">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

   >[!NOTE]
   ><span data-ttu-id="cb321-122">No puede hacer clic en notificaciones con un estado **Correcto** o **En curso**.</span><span class="sxs-lookup"><span data-stu-id="cb321-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="cb321-123">Esto hace que se abra la hoja **Detalles de la notificación**.</span><span class="sxs-lookup"><span data-stu-id="cb321-123">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="cb321-124">Utilice esta información para conocer más detalles acerca del problema.</span><span class="sxs-lookup"><span data-stu-id="cb321-124">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="cb321-125">Si aún necesita ayuda, también puede compartir esta información con un ingeniero de soporte técnico o el grupo de producto para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="cb321-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="cb321-126">Haga clic en el **icono de copia** situado a la derecha del cuadro de texto **Copiar error** para copiar todos los detalles de la notificación para compartirlos con un ingeniero de soporte técnico o un grupo de producto.</span><span class="sxs-lookup"><span data-stu-id="cb321-126">Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="cb321-127">Obtención de ayuda mediante el envío de detalles de la notificación a un ingeniero de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="cb321-127">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="cb321-128">Es muy importante que comparta **todos los detalles que se muestran a continuación** con un ingeniero de soporte técnico si necesita ayuda, para que pueda ayudarle rápidamente.</span><span class="sxs-lookup"><span data-stu-id="cb321-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="cb321-129">Puede hacer esto fácilmente **realizando una captura de pantalla** o haciendo clic en el **icono Copiar error**, que se encuentra a la derecha del cuadro de texto **Copiar error**.</span><span class="sxs-lookup"><span data-stu-id="cb321-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="cb321-130">Explicación de los detalles de la notificación</span><span class="sxs-lookup"><span data-stu-id="cb321-130">Notification Details Explained</span></span>

<span data-ttu-id="cb321-131">A continuación se explica más en profundidad lo que significa cada uno de los elementos de notificación y se dan ejemplos de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="cb321-131">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="cb321-132">Elementos esenciales de notificación</span><span class="sxs-lookup"><span data-stu-id="cb321-132">Essential Notification Items</span></span>

-   <span data-ttu-id="cb321-133">**Título**: el título descriptivo de la notificación</span><span class="sxs-lookup"><span data-stu-id="cb321-133">**Title** – the descriptive title of the notification</span></span>
   *  <span data-ttu-id="cb321-134">Por ejemplo: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="cb321-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="cb321-135">**Descripción**: la descripción de lo que se produjo como resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="cb321-135">**Description** – the description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="cb321-136">Por ejemplo: **la dirección url interna especificada ya se está usando en otra aplicación**</span><span class="sxs-lookup"><span data-stu-id="cb321-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="cb321-137">**Identificador de notificación**: el identificador único de la notificación</span><span class="sxs-lookup"><span data-stu-id="cb321-137">**Notification Id** – the unique id of the notification</span></span>

   *  <span data-ttu-id="cb321-138">Por ejemplo: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="cb321-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="cb321-139">**Identificador de solicitud de cliente**: el identificador de solicitud específico generado por el explorador</span><span class="sxs-lookup"><span data-stu-id="cb321-139">**Client Request Id** – the specific request id made by your browser</span></span>

   *  <span data-ttu-id="cb321-140">Por ejemplo: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="cb321-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="cb321-141">**Marca de tiempo UTC**: la marca de tiempo durante la que tuvo lugar la notificación, en formato UTC</span><span class="sxs-lookup"><span data-stu-id="cb321-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

   *  <span data-ttu-id="cb321-142">Por ejemplo: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="cb321-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="cb321-143">**Identificador de transacción interno**: el identificador interno que podemos utilizar para buscar el error en nuestros sistemas</span><span class="sxs-lookup"><span data-stu-id="cb321-143">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

   *  <span data-ttu-id="cb321-144">Por ejemplo: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="cb321-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="cb321-145">**UPN**: el usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="cb321-145">**UPN** – the user who performed the operation</span></span>

   *  <span data-ttu-id="cb321-146">Por ejemplo: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="cb321-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="cb321-147">**Identificador de inquilino**: el identificador único del inquilino del que formaba parte el usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="cb321-147">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

   *  <span data-ttu-id="cb321-148">Por ejemplo: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="cb321-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="cb321-149">**Identificador de objeto de usuario**: el identificador único del usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="cb321-149">**User object Id** – the unique ID of the user who performed the operation</span></span>

 *  <span data-ttu-id="cb321-150">Por ejemplo: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="cb321-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="cb321-151">Elementos detallados de notificación</span><span class="sxs-lookup"><span data-stu-id="cb321-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="cb321-152">**Nombre para mostrar**: **(puede estar vacío)** un nombre para mostrar más detallado del error</span><span class="sxs-lookup"><span data-stu-id="cb321-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

  *  <span data-ttu-id="cb321-153">Por ejemplo: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="cb321-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="cb321-154">**Estado**: el estado específico de la notificación</span><span class="sxs-lookup"><span data-stu-id="cb321-154">**Status** – the specific status of the notification</span></span>

   *  <span data-ttu-id="cb321-155">Por ejemplo: **Error**</span><span class="sxs-lookup"><span data-stu-id="cb321-155">Example – **Failed**</span></span>

-   <span data-ttu-id="cb321-156">**Identificador de objeto**: **(puede estar vacío)** el identificador del objeto en el que se realizó la operación</span><span class="sxs-lookup"><span data-stu-id="cb321-156">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

   *  <span data-ttu-id="cb321-157">Por ejemplo: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="cb321-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="cb321-158">**Detalles**: la descripción detallada de lo que se produjo como resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="cb321-158">**Details** – the detailed description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="cb321-159">Por ejemplo: **la dirección url interna 'http://bing.com/' no es válida puesto que ya está en uso**</span><span class="sxs-lookup"><span data-stu-id="cb321-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="cb321-160">**Copiar error**: haga clic en el **icono de copia** situado a la derecha del cuadro de texto **Copiar error** para copiar todos los detalles de la notificación para compartirlos con un ingeniero de soporte técnico o un grupo de producto</span><span class="sxs-lookup"><span data-stu-id="cb321-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

   *  <span data-ttu-id="cb321-161">Por ejemplo, ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="cb321-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb321-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb321-162">Next steps</span></span>
[<span data-ttu-id="cb321-163">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb321-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



