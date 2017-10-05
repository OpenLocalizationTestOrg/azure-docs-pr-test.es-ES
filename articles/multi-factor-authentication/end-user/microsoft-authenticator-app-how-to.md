---
title: "Aplicación Microsoft Authenticator para teléfonos móviles | Microsoft Docs"
description: "Aprenda a actualizar a la versión más reciente de Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="d5b85-103">Introducción a la aplicación Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="d5b85-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="d5b85-104">La aplicación Microsoft Authenticator proporciona un nivel de seguridad adicional para su cuenta profesional o educativa (por ejemplo, bsimon@contoso.com) o su cuenta de Microsoft (por ejemplo, bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="d5b85-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="d5b85-105">La aplicación funciona de una de estas dos formas:</span><span class="sxs-lookup"><span data-stu-id="d5b85-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="d5b85-106">**Notificación**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-106">**Notification**.</span></span> <span data-ttu-id="d5b85-107">La aplicación puede ayudar a impedir el acceso no autorizado a las cuentas y detener las transacciones fraudulentas mediante el envío de una notificación al smartphone o a la tableta.</span><span class="sxs-lookup"><span data-stu-id="d5b85-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="d5b85-108">Solo tiene que ver la notificación y, si es legítima, seleccionar **Comprobar**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="d5b85-109">De lo contrario, seleccione **Denegar**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="d5b85-110">**Código de comprobación**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-110">**Verification code**.</span></span> <span data-ttu-id="d5b85-111">La aplicación puede utilizarse como token de software para generar un código de comprobación de OAuth.</span><span class="sxs-lookup"><span data-stu-id="d5b85-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="d5b85-112">Después de escribir el nombre de usuario y la contraseña, especifique el código que facilita la aplicación en la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d5b85-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="d5b85-113">El código de comprobación es una forma adicional de autenticación.</span><span class="sxs-lookup"><span data-stu-id="d5b85-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="d5b85-114">La aplicación Microsoft Authenticator sustituye a la aplicación Azure Authenticator.</span><span class="sxs-lookup"><span data-stu-id="d5b85-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="d5b85-115">La aplicación Azure Authenticator sigue funcionando, pero, si decide dar el paso a la nueva aplicación Microsoft Authenticator, este artículo puede servirle de ayuda.</span><span class="sxs-lookup"><span data-stu-id="d5b85-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="d5b85-116">Suscripción a la comprobación en dos pasos</span><span class="sxs-lookup"><span data-stu-id="d5b85-116">Opt in for two-step verification</span></span>

<span data-ttu-id="d5b85-117">La aplicación Microsoft Authenticator no funciona por sí misma.</span><span class="sxs-lookup"><span data-stu-id="d5b85-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="d5b85-118">Configure cada una de sus cuentas para que se le solicite un segundo método de comprobación después de iniciar sesión con su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="d5b85-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="d5b85-119">En cuentas profesionales o educativas, por lo habitual esta característica no tiene que elegirla.</span><span class="sxs-lookup"><span data-stu-id="d5b85-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="d5b85-120">En cambio, es el administrador de seguridad el que tiene que suscribirse en su nombre y, después, le envía una notificación para que registre los métodos de comprobación de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="d5b85-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="d5b85-121">Si este escenario se aplica en su caso, obtenga información en [¿Qué relevancia tiene Azure Multi-Factor Authentication para mí?](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="d5b85-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="d5b85-122">En una cuenta personal, debe configurar la comprobación en dos pasos usted mismo.</span><span class="sxs-lookup"><span data-stu-id="d5b85-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="d5b85-123">Si tiene una cuenta de Microsoft, esos pasos están disponibles en [Acerca de la verificación en dos pasos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="d5b85-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="d5b85-124">También puede usar Microsoft Authenticator con cuentas que no sean de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d5b85-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="d5b85-125">Aunque es posible que llamen a la característica de comprobación en dos de otra manera, lo más seguro es que la encuentre en la configuración de seguridad o de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d5b85-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="d5b85-126">Instalación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d5b85-126">Install the app</span></span>
<span data-ttu-id="d5b85-127">La aplicación Microsoft Authenticator está disponible para [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072) e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="d5b85-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="d5b85-128">Incorporación de cuentas a la aplicación</span><span class="sxs-lookup"><span data-stu-id="d5b85-128">Add accounts to the app</span></span>
<span data-ttu-id="d5b85-129">Siga uno de los procedimientos siguientes para cada cuenta que desee agregar a la aplicación Microsoft Authenticator:</span><span class="sxs-lookup"><span data-stu-id="d5b85-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="d5b85-130">Incorporación de una cuenta Microsoft personal a la aplicación</span><span class="sxs-lookup"><span data-stu-id="d5b85-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="d5b85-131">Para una cuenta Microsoft personal (una que use para iniciar sesión en Outlook.com, Xbox, Skype, etc.), lo único que debe hacer es iniciar sesión en ella, en la aplicación Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="d5b85-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="d5b85-132">Incorporación de una cuenta profesional o educativa a la aplicación con el escáner de códigos QR</span><span class="sxs-lookup"><span data-stu-id="d5b85-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="d5b85-133">Vaya a la pantalla de configuración de comprobación de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d5b85-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="d5b85-134">Para información sobre cómo ir a esta pantalla, consulte la sección sobre el [cambio de la configuración de seguridad](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="d5b85-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="d5b85-135">Active la casilla situada junto a **Aplicación Authenticator** y luego seleccione **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![Botón Configurar en la pantalla de configuración de la comprobación de seguridad](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="d5b85-137">Aparecerá una pantalla con un código QR.</span><span class="sxs-lookup"><span data-stu-id="d5b85-137">This brings up a screen with a QR code on it.</span></span>

    ![Pantalla que proporciona el código QR](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="d5b85-139">Abra la aplicación Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="d5b85-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="d5b85-140">En la pantalla **Cuentas**, seleccione **+** y especifique que quiere agregar una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="d5b85-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="d5b85-141">Utilice la cámara para digitalizar el código QR y seleccione **Listo** para cerrar la pantalla de código QR.</span><span class="sxs-lookup"><span data-stu-id="d5b85-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="d5b85-142">Si la cámara no funciona correctamente, puede [escribir manualmente la dirección URL y el código QR](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="d5b85-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="d5b85-143">Cuando la aplicación muestra el nombre de cuenta con un código de seis dígitos debajo de él, ya ha terminado.</span><span class="sxs-lookup"><span data-stu-id="d5b85-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Pantalla Cuentas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="d5b85-145">Incorporación manual de una cuenta a la aplicación</span><span class="sxs-lookup"><span data-stu-id="d5b85-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="d5b85-146">Vaya a la pantalla de configuración de comprobación de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d5b85-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="d5b85-147">Para información sobre cómo ir a esta pantalla, consulte la sección sobre el [cambio de la configuración de seguridad](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d5b85-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="d5b85-148">Seleccione **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-148">Select **Configure**.</span></span>

    ![Botón Configurar en la pantalla de configuración de la comprobación de seguridad](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="d5b85-150">Aparecerá una pantalla con un código QR.</span><span class="sxs-lookup"><span data-stu-id="d5b85-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="d5b85-151">Anote la dirección URL y el código.</span><span class="sxs-lookup"><span data-stu-id="d5b85-151">Note the code and URL.</span></span>

    ![Pantalla que proporciona el código QR y la dirección URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="d5b85-153">Abra la aplicación Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="d5b85-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="d5b85-154">En la pantalla **Cuentas**, seleccione **+** y especifique que quiere agregar una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="d5b85-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="d5b85-155">En el digitalizador, elija **escribir el código manualmente**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-155">In the scanner, select **enter code manually**.</span></span>

    ![Pantalla para digitalizar un código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="d5b85-157">En la aplicación, escriba el código y la dirección URL en los cuadros correspondientes y luego seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![Pantalla para escribir el código y la dirección URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="d5b85-159">Cuando la aplicación muestra el nombre de cuenta con un código de seis dígitos debajo de él, ya ha terminado.</span><span class="sxs-lookup"><span data-stu-id="d5b85-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Pantalla Cuentas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="d5b85-161">Incorporación de una cuenta a la aplicación con Touch ID</span><span class="sxs-lookup"><span data-stu-id="d5b85-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="d5b85-162">La aplicación Microsoft Authenticator de iOS es compatible con Touch ID.</span><span class="sxs-lookup"><span data-stu-id="d5b85-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="d5b85-163">Azure Multi-Factor Authentication permite a las organizaciones pedir un PIN para los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d5b85-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="d5b85-164">Con Touch ID, los usuarios de iOS no tienen por qué escribir un PIN.</span><span class="sxs-lookup"><span data-stu-id="d5b85-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="d5b85-165">En su lugar, pueden digitalizar su huella y seleccionar **Aprobar**.</span><span class="sxs-lookup"><span data-stu-id="d5b85-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="d5b85-166">Configurar Touch ID con Microsoft Authenticator es sencillo.</span><span class="sxs-lookup"><span data-stu-id="d5b85-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="d5b85-167">Un PIN supone un reto de comprobación normal.</span><span class="sxs-lookup"><span data-stu-id="d5b85-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="d5b85-168">Si el dispositivo es compatible con Touch ID, Microsoft Authenticator lo configura automáticamente para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="d5b85-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Comprobación de la configuración de Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="d5b85-170">A partir de ese momento, cuando se requiera que compruebe el inicio de sesión, seleccione la notificación push recibida y digitalice la huella dactilar en lugar de escribir su PIN.</span><span class="sxs-lookup"><span data-stu-id="d5b85-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Notificación push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="d5b85-172">Uso de la aplicación al iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="d5b85-172">Use the app when you sign in</span></span>

<span data-ttu-id="d5b85-173">Después de que la cuenta se agregue a la aplicación, puede que se le solicite que realice una comprobación de prueba para asegurarse de que todo está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d5b85-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="d5b85-174">Después de eso, habrá terminado.</span><span class="sxs-lookup"><span data-stu-id="d5b85-174">After that, you're done!</span></span> <span data-ttu-id="d5b85-175">No es necesario hacer nada más hasta la próxima vez que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="d5b85-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="d5b85-176">Si eligió usar códigos de comprobación en la aplicación, comienza a verlos en la página principal.</span><span class="sxs-lookup"><span data-stu-id="d5b85-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="d5b85-177">Como cambian cada 30 segundos, siempre tendrá un código nuevo cuando lo necesite.</span><span class="sxs-lookup"><span data-stu-id="d5b85-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="d5b85-178">Pero no tiene que hacer nada con ellos hasta que inicie sesión y se le solicite que escriba un código de comprobación.</span><span class="sxs-lookup"><span data-stu-id="d5b85-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  