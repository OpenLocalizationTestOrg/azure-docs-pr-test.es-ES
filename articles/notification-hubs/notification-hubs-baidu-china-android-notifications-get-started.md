---
title: aaaGet a trabajar con los centros de notificaciones de Azure mediante Baidu | Documentos de Microsoft
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toopush notificaciones tooAndroid dispositivos que utilizan Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="5d546-103">Introducción a Notification Hubs con Baidu</span><span class="sxs-lookup"><span data-stu-id="5d546-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5d546-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5d546-104">Overview</span></span>
<span data-ttu-id="5d546-105">Inserción de Baidu en la nube es un servicio de nube chino que pueden usar dispositivos de toomobile de notificaciones de inserción de toosend.</span><span class="sxs-lookup"><span data-stu-id="5d546-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="5d546-106">Este servicio es útil en China, donde entregar notificaciones de inserción tooAndroid es compleja debido a la presencia de Hola de tiendas de aplicaciones diferentes e inserte contenido de servicios, además toohello disponibilidad de dispositivos Android que no están conectado normalmente tooGCM (Google La nube de mensajería).</span><span class="sxs-lookup"><span data-stu-id="5d546-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d546-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5d546-107">Prerequisites</span></span>
<span data-ttu-id="5d546-108">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5d546-108">This tutorial requires:</span></span>

* <span data-ttu-id="5d546-109">SDK de Android (se supone que usa Eclipse), que puede descargar desde hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sitio Android</a></span><span class="sxs-lookup"><span data-stu-id="5d546-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="5d546-110">[Android SDK para Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="5d546-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="5d546-111">[Baidu Push Android SDK]</span><span class="sxs-lookup"><span data-stu-id="5d546-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="5d546-112">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d546-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="5d546-113">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5d546-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5d546-114">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="5d546-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="5d546-115">Creación de una cuenta de Baidu</span><span class="sxs-lookup"><span data-stu-id="5d546-115">Create a Baidu account</span></span>
<span data-ttu-id="5d546-116">toouse Baidu, debe tener una cuenta de Baidu.</span><span class="sxs-lookup"><span data-stu-id="5d546-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="5d546-117">Si ya tiene una, inicie sesión en toohello [Baidu portal] y omitir el paso siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="5d546-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="5d546-118">En caso contrario, vea Hola siguiendo las instrucciones sobre cómo toocreate una cuenta de Baidu.</span><span class="sxs-lookup"><span data-stu-id="5d546-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="5d546-119">Vaya toohello [Baidu portal] y haga clic en hello**登录**(**inicio de sesión**) vínculo.</span><span class="sxs-lookup"><span data-stu-id="5d546-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="5d546-120">Haga clic en**立即注册**toostart proceso de registro de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="5d546-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="5d546-121">Escriba los detalles de hello necesario, teléfono o correo electrónico código de comprobación, la contraseña y la dirección y haga clic en **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="5d546-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="5d546-122">Se le enviará una dirección de correo electrónico toohello de correo electrónico que escribió con un vínculo tooactivate su cuenta de Baidu.</span><span class="sxs-lookup"><span data-stu-id="5d546-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="5d546-123">Inicie sesión en la cuenta de correo electrónico de tooyour, abra el correo electrónico de activación de Baidu hello y haga clic en tooactivate de vínculo de activación de Hola su cuenta de Baidu.</span><span class="sxs-lookup"><span data-stu-id="5d546-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="5d546-124">Una vez que tenga una cuenta de Baidu activada, inicie sesión en toohello [Baidu portal].</span><span class="sxs-lookup"><span data-stu-id="5d546-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="5d546-125">Registro como desarrollador de Baidu</span><span class="sxs-lookup"><span data-stu-id="5d546-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="5d546-126">Una vez que han iniciado sesión en toohello [Baidu portal], haga clic en**更多 >>** (**más**).</span><span class="sxs-lookup"><span data-stu-id="5d546-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="5d546-127">Desplácese hacia abajo en hello**站长与开发者服务 (Administrador de Web y servicios para desarrolladores)** sección y haga clic en**百度开放云平台**(**Baidu abrir plataforma de nube**).</span><span class="sxs-lookup"><span data-stu-id="5d546-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="5d546-128">En la página siguiente de hello, haga clic en**开发者服务**(**servicios para desarrolladores**) en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="5d546-129">En la página siguiente de hello, haga clic en**注册开发者**(**desarrolladores registrado**) desde el menú de hello en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="5d546-130">Escriba su nombre, una descripción y un número de teléfono móvil para recibir un mensaje de texto de verificación y, a continuación, haga clic en **送验证码** (**Enviar código de verificación**).</span><span class="sxs-lookup"><span data-stu-id="5d546-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="5d546-131">Para números de teléfono internacional, es necesario código de país de hello tooenclose entre paréntesis.</span><span class="sxs-lookup"><span data-stu-id="5d546-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="5d546-132">Por ejemplo, para un número de Estados Unidos, es **(1) 1234567890**.</span><span class="sxs-lookup"><span data-stu-id="5d546-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="5d546-133">A continuación, debe recibir un mensaje de texto con un número de verificación, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="5d546-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="5d546-134">Introducir número de verificación de Hola de mensaje de saludo en**验证码**(**código de confirmación**).</span><span class="sxs-lookup"><span data-stu-id="5d546-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="5d546-135">Por último, completar el registro de desarrollador de hello Aceptar hello Baidu contrato y haga clic en**提交**(**enviar**).</span><span class="sxs-lookup"><span data-stu-id="5d546-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="5d546-136">Verá Hola después de la página de finalización correcta del registro:</span><span class="sxs-lookup"><span data-stu-id="5d546-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="5d546-137">Creación de un proyecto de inserción de nube Baidu</span><span class="sxs-lookup"><span data-stu-id="5d546-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="5d546-138">Cuando se crea un proyecto de inserción de nube Baidu, recibirá el identificador de la aplicación, la clave de API y la clave secreta.</span><span class="sxs-lookup"><span data-stu-id="5d546-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="5d546-139">Una vez que han iniciado sesión en toohello [Baidu portal], haga clic en**更多 >>** (**más**).</span><span class="sxs-lookup"><span data-stu-id="5d546-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="5d546-140">Desplácese hacia abajo en hello**站长与开发者服务**(**administrador del sitio Web y servicios para desarrolladores**) sección y haga clic en**百度开放云平台**(**Baidu abrir plataforma de nube**).</span><span class="sxs-lookup"><span data-stu-id="5d546-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="5d546-141">En la página siguiente de hello, haga clic en**开发者服务**(**servicios para desarrolladores**) en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="5d546-142">En la página siguiente de hello, haga clic en**云推送**(**de inserción en la nube**) de hello**云服务**(**servicios en la nube**) sección.</span><span class="sxs-lookup"><span data-stu-id="5d546-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="5d546-143">Una vez haya un desarrollador registrado, vea**管理控制台**(**Management Console**) en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="5d546-144">Haga clic en **开发者服务管理** (**Administración de servicios de desarrolladores**).</span><span class="sxs-lookup"><span data-stu-id="5d546-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="5d546-145">En la página siguiente de hello, haga clic en**创建工程**(**crear proyecto**).</span><span class="sxs-lookup"><span data-stu-id="5d546-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="5d546-146">Escriba un nombre de aplicación y haga clic en **创建** (**Crear**).</span><span class="sxs-lookup"><span data-stu-id="5d546-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="5d546-147">Tras crear correctamente un proyecto de Baidu Cloud Push, se mostrará una página con el **AppID**, la **clave de API** y la **clave secreta**.</span><span class="sxs-lookup"><span data-stu-id="5d546-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="5d546-148">Tome nota de la clave de API de Hola y de clave secreta, que se utilizará más adelante.</span><span class="sxs-lookup"><span data-stu-id="5d546-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="5d546-149">Configurar el proyecto de hello las notificaciones de inserción, haga clic en**云推送**(**nube inserción**) en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="5d546-150">En la página siguiente de hello, haga clic en hello**推送设置**(**Insertar configuración**) botón.</span><span class="sxs-lookup"><span data-stu-id="5d546-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="5d546-151">En la página de configuración de hello, agregue el nombre de paquete de Hola que va a usar en el proyecto Android en hello**应用包名**(**paquete de aplicación**) campo y, a continuación, haga clic en**保存设置**() **Guardar**).</span><span class="sxs-lookup"><span data-stu-id="5d546-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="5d546-152">Vea hello**保存成功!** (**Guardado correctamente**).</span><span class="sxs-lookup"><span data-stu-id="5d546-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="5d546-153">Configuración de su Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="5d546-153">Configure your notification hub</span></span>
1. <span data-ttu-id="5d546-154">Inicie sesión en toohello [Portal clásico de Azure]y, a continuación, haga clic en **+ nuevo** final Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="5d546-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="5d546-155">Haga clic sucesivamente en **App Services**, **Service Bus**, **Centro de notificaciones** y, finalmente, en **Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="5d546-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="5d546-156">Proporcione un nombre para su **centro de notificaciones**, seleccione hello **región** hello y **Namespace** donde se creará este centro de notificaciones y, a continuación, haga clic en  **Crear un nuevo centro de notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="5d546-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="5d546-157">Haga clic en el espacio de nombres de hello en el que se creó el centro de notificaciones y, a continuación, haga clic en **centros de notificaciones** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="5d546-158">Centro de notificaciones de hello SELECT que creó y, a continuación, haga clic en **configurar** de menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="5d546-159">Desplácese hacia abajo toohello **configuración de notificaciones de baidu** sección y escriba la clave de API de hello y una clave secreta que obtuvo de la consola de Baidu Hola previamente para su proyecto de inserción de la nube de Baidu.</span><span class="sxs-lookup"><span data-stu-id="5d546-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="5d546-160">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5d546-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="5d546-161">Haga clic en hello **panel** pestaña princip Hola Hola central de notificaciones y, a continuación, haga clic en **ver cadenas de conexión**.</span><span class="sxs-lookup"><span data-stu-id="5d546-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="5d546-162">Tome nota de hello **DefaultListenSharedAccessSignature** y **DefaultFullSharedAccessSignature** de hello **acceso a la información de conexión** ventana.</span><span class="sxs-lookup"><span data-stu-id="5d546-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="5d546-163">Conectar el centro de notificaciones de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="5d546-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="5d546-164">En Eclipse ADT, cree un nuevo proyecto de Android (**File** > **New** > **Android Application Project**).</span><span class="sxs-lookup"><span data-stu-id="5d546-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="5d546-165">Escriba un **nombre de la aplicación** y asegúrese de que hello **mínimo necesario SDK** versión se establece demasiado**API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="5d546-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="5d546-166">Haga clic en **siguiente** y continuar después de Asistente de hello hasta hello **Crear actividad** aparecerá la ventana.</span><span class="sxs-lookup"><span data-stu-id="5d546-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="5d546-167">Asegúrese de que **actividad en blanco** está seleccionada y, por último, seleccione **finalizar** toocreate una nueva aplicación de Android.</span><span class="sxs-lookup"><span data-stu-id="5d546-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="5d546-168">Asegúrese de que ese hello **destino de compilación del proyecto** se ha establecido correctamente.</span><span class="sxs-lookup"><span data-stu-id="5d546-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="5d546-169">Descargar archivo de bases de datos centrales de notificación de 0.4.jar de Hola de hello **archivos** ficha de hello [notificación-concentradores-Android-SDK en Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="5d546-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="5d546-170">Agregar Hola archivo toohello **bibliotecas** carpeta del proyecto de Eclipse y actualización hello *bibliotecas* carpeta.</span><span class="sxs-lookup"><span data-stu-id="5d546-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="5d546-171">Descargue y descomprima hello [Baidu Push Android SDK], abra hello **bibliotecas** carpeta y, a continuación, Hola copia **pushservice x.y.z** jar hello y archivo **armeabi**  &  **mips** carpetas en hello **bibliotecas** carpeta de la aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="5d546-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="5d546-172">Abra hello **AndroidManifest.xml** archivos de sus Android del proyecto y agregar permisos de hello requeridos por hello Baidu SDK.</span><span class="sxs-lookup"><span data-stu-id="5d546-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="5d546-173">Agregar Hola **android: name** propiedad tooyour **aplicación** elemento **AndroidManifest.xml**, reemplazando *NombreDelProyecto* (para ejemplo, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="5d546-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="5d546-174">Asegúrese de que este nombre del proyecto coincide con hello uno que configuró en la consola de Baidu Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="5d546-175">Agregar Hola siguiente configuración en el elemento de la aplicación hello después hello **. MainActivity** elemento de actividad, reemplazando *NombreDelProyecto* (por ejemplo, **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="5d546-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="5d546-176">Agregue una nueva clase denominada **ConfigurationSettings.java** toohello proyecto.</span><span class="sxs-lookup"><span data-stu-id="5d546-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="5d546-177">Agregue Hola después tooit de código:</span><span class="sxs-lookup"><span data-stu-id="5d546-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="5d546-178">Establecer valor de Hola de **API_KEY** con recuperar desde el proyecto de nube de Baidu Hola anteriormente, **NotificationHubName** con su nombre de base de datos central de notificaciones de hello Portal clásico de Azure y  **NotificationHubConnectionString** con DefaultListenSharedAccessSignature de hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d546-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="5d546-179">Agregue una nueva clase denominada **DemoApplication.java**y agregue Hola después tooit de código:</span><span class="sxs-lookup"><span data-stu-id="5d546-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="5d546-180">Agregue otra nueva clase denominada **MyPushMessageReceiver.java**y agregue Hola después tooit de código.</span><span class="sxs-lookup"><span data-stu-id="5d546-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="5d546-181">Es clase hello que identificadores Hola notificaciones de inserción que se reciben del servidor de inserción de Baidu Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="5d546-182">Abra **MainActivity.java**y agregue Hola después toohello **onCreate** método:</span><span class="sxs-lookup"><span data-stu-id="5d546-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="5d546-183">Abra Hola siguiendo las instrucciones de importación en la parte superior de hello:</span><span class="sxs-lookup"><span data-stu-id="5d546-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="5d546-184">Enviar notificaciones tooyour aplicación</span><span class="sxs-lookup"><span data-stu-id="5d546-184">Send notifications tooyour app</span></span>
<span data-ttu-id="5d546-185">Puede probar rápidamente recibir notificaciones en la aplicación mediante el envío de notificaciones en hello [portal de Azure](https://portal.azure.com/) con hello **enviar** situado en el centro de notificaciones de hello, como se muestra en hello después de pantalla:</span><span class="sxs-lookup"><span data-stu-id="5d546-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="5d546-186">Las notificaciones push se envían normalmente en un servicio back-end como Mobile Services o ASP.NET mediante una biblioteca compatible.</span><span class="sxs-lookup"><span data-stu-id="5d546-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="5d546-187">Si una biblioteca no está disponible para el back-end, puede usar API de REST de hello toosend directamente los mensajes de notificación.</span><span class="sxs-lookup"><span data-stu-id="5d546-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="5d546-188">En este tutorial, se mantenga simple y solo muestra probar la aplicación cliente mediante el envío de notificaciones mediante Hola .NET SDK centrales de notificaciones en una aplicación de consola en lugar de un servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="5d546-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="5d546-189">Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial como paso siguiente de Hola para enviar notificaciones desde un back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5d546-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="5d546-190">Sin embargo, Hola siguiendo métodos puede utilizarse para enviar notificaciones:</span><span class="sxs-lookup"><span data-stu-id="5d546-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="5d546-191">**Interfaz REST**: admitir la notificación en cualquier plataforma de back-end mediante hello [interfaz REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d546-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="5d546-192">**SDK de .NET de Microsoft Azure notificación concentradores**: Hola Administrador de paquetes de Nuget para Visual Studio, ejecutar [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="5d546-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="5d546-193">**Node.js**: [cómo toouse centros de notificaciones de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="5d546-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="5d546-194">**Aplicaciones móviles**: para obtener un ejemplo de cómo toosend notificaciones desde un back-end de aplicaciones de Mobile de servicio de aplicación de Azure que se integra con centros de notificaciones, consulte [Agregar aplicación móvil de inserción notificaciones tooyour](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="5d546-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="5d546-195">**Java / PHP**: para obtener un ejemplo de cómo toosend notificaciones mediante el uso de hello las API de REST, vea "cómo toouse centros de notificaciones de Java y PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="5d546-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="5d546-196">(Opcional) Envío de notificaciones desde una aplicación de consola .NET</span><span class="sxs-lookup"><span data-stu-id="5d546-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="5d546-197">En esta sección, mostramos cómo enviar una notificación mediante una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="5d546-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="5d546-198">Cree una aplicación de consola nueva de Visual C#:</span><span class="sxs-lookup"><span data-stu-id="5d546-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="5d546-199">En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5d546-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="5d546-200">Esta instrucción agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="5d546-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="5d546-201">Archivo abierto hello **Program.cs** y agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="5d546-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="5d546-202">En su `Program` clase, agregue Hola siguiente método y reemplace *DefaultFullSharedAccessSignatureSASConnectionString* y *NotificationHubName* con valores de hello que tenga.</span><span class="sxs-lookup"><span data-stu-id="5d546-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="5d546-203">Agregar Hola siguiendo las líneas en el **Main** método:</span><span class="sxs-lookup"><span data-stu-id="5d546-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="5d546-204">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5d546-204">Test your app</span></span>
<span data-ttu-id="5d546-205">tootest conectar esta aplicación con un teléfono real, simplemente Hola equipo tooyour de teléfono mediante un cable USB.</span><span class="sxs-lookup"><span data-stu-id="5d546-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="5d546-206">Esta acción carga la aplicación en el teléfono de hello adjuntada.</span><span class="sxs-lookup"><span data-stu-id="5d546-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="5d546-207">tootest esta aplicación con el emulador de Windows hello, en la barra de herramientas superior de hello Eclipse, haga clic en ejecutar **ejecutar**y, a continuación, seleccione la aplicación: se inicia el emulador de Windows hello, carga, y se ejecuta Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d546-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="5d546-208">aplicación Hello recupera hello 'userId' y 'channelId' de hello servicio de notificaciones de inserción de Baidu y se registra con el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="5d546-209">toosend una notificación de prueba, puede utilizar la pestaña depurar de Hola de hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d546-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="5d546-210">Si ha creado la aplicación de consola .NET de Hola para Visual Studio, simplemente presione tecla F5 de hello en aplicaciones de Visual Studio toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="5d546-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="5d546-211">aplicación Hello envía una notificación que aparece en el área de notificación superior de Hola de su dispositivo o emulador.</span><span class="sxs-lookup"><span data-stu-id="5d546-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Android SDK para Mobile Services]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Portal clásico de Azure]: https://manage.windowsazure.com/
[Baidu portal]: http://www.baidu.com/
