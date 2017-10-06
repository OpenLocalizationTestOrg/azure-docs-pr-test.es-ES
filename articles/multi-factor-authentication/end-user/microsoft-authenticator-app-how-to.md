---
title: "Authenticator de aaaMicrosoft para teléfonos móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupgrade toohello versión más reciente de Azure Authenticator."
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
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="f7460-103">Introducción a la aplicación de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="f7460-103">Get started with hello Microsoft Authenticator app</span></span>
<span data-ttu-id="f7460-104">aplicación Microsoft Authenticator Hello proporciona un nivel adicional de seguridad en su cuenta profesional o educativa (por ejemplo, bsimon@contoso.com) o la cuenta de Microsoft (por ejemplo, bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="f7460-104">hello Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="f7460-105">funciona de la aplicación Hello en uno de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="f7460-105">hello app works in one of two ways:</span></span>

* <span data-ttu-id="f7460-106">**Notificación**.</span><span class="sxs-lookup"><span data-stu-id="f7460-106">**Notification**.</span></span> <span data-ttu-id="f7460-107">aplicación Hello puede ayudar a evitar accesos no autorizados tooaccounts y detener las transacciones fraudulentas insertando una tableta o smartphone tooyour de notificación.</span><span class="sxs-lookup"><span data-stu-id="f7460-107">hello app can help prevent unauthorized access tooaccounts and stop fraudulent transactions by pushing a notification tooyour smartphone or tablet.</span></span> <span data-ttu-id="f7460-108">Simplemente ver notificación hello y, si es legítima, seleccione **compruebe**.</span><span class="sxs-lookup"><span data-stu-id="f7460-108">Simply view hello notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="f7460-109">De lo contrario, seleccione **Denegar**.</span><span class="sxs-lookup"><span data-stu-id="f7460-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="f7460-110">**Código de comprobación**.</span><span class="sxs-lookup"><span data-stu-id="f7460-110">**Verification code**.</span></span> <span data-ttu-id="f7460-111">aplicación Hello puede usarse como un software de token toogenerate un código de comprobación de OAuth.</span><span class="sxs-lookup"><span data-stu-id="f7460-111">hello app can be used as a software token toogenerate an OAuth verification code.</span></span> <span data-ttu-id="f7460-112">Después de escribir el nombre de usuario y la contraseña, se escribe código de hello proporcionada por la aplicación hello en pantalla de inicio de sesión de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="f7460-112">After you enter your username and password, you enter hello code provided by hello app into hello sign-in screen.</span></span> <span data-ttu-id="f7460-113">código de comprobación de Hello proporciona una segunda forma de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f7460-113">hello verification code provides a second form of authentication.</span></span>

<span data-ttu-id="f7460-114">aplicación de Microsoft Authenticator Hello reemplaza la aplicación Azure Authenticator de hello.</span><span class="sxs-lookup"><span data-stu-id="f7460-114">hello Microsoft Authenticator app replaces hello Azure Authenticator app.</span></span> <span data-ttu-id="f7460-115">Hello Azure Authenticator aplicación todavía funciona, pero si decide toomove toohello la nueva aplicación de Microsoft Authenticator, este artículo le puede ayudar.</span><span class="sxs-lookup"><span data-stu-id="f7460-115">hello Azure Authenticator app still works, but if you decide toomove toohello new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="f7460-116">Suscripción a la comprobación en dos pasos</span><span class="sxs-lookup"><span data-stu-id="f7460-116">Opt in for two-step verification</span></span>

<span data-ttu-id="f7460-117">aplicación de Microsoft Authenticator Hello no funciona por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="f7460-117">hello Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="f7460-118">Configurar cada uno de los tooprompt de cuentas de un segundo método de comprobación después de iniciar sesión con su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="f7460-118">Configure each of your accounts tooprompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="f7460-119">Para una cuenta profesional o educativa, no por lo general obtendrá toochoose esta característica por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="f7460-119">For a work or school account, you don't usually get toochoose this feature for yourself.</span></span> <span data-ttu-id="f7460-120">En su lugar, un administrador de seguridad opts en su nombre y, a continuación, notifica a métodos de comprobación de tooregister para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="f7460-120">Instead, a security administrator opts in on your behalf and then notifies you tooregister verification methods for your account.</span></span> <span data-ttu-id="f7460-121">Si esta situación aplica tooyou, obtenga más información en [¿qué significa la autenticación multifactor Azure para mí](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="f7460-121">If this scenario applies tooyou, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="f7460-122">Para una cuenta personal, deberá tooset configuraste la verificación por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="f7460-122">For a personal account, you need tooset up two-step verification for yourself.</span></span> <span data-ttu-id="f7460-123">Si tiene una cuenta de Microsoft, esos pasos están disponibles en [Acerca de la verificación en dos pasos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="f7460-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="f7460-124">También puede utilizar Microsoft Authenticator Hola con cuentas de otros fabricantes.</span><span class="sxs-lookup"><span data-stu-id="f7460-124">You can also use hello Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="f7460-125">Puede llamar a Hola característica algo distinto de verificación en dos pasos, pero debe ser capaz de toofind en configuración de seguridad o inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f7460-125">They may call hello feature something other than two-step verification, but you should be able toofind it under security or sign-in settings.</span></span> 

## <a name="install-hello-app"></a><span data-ttu-id="f7460-126">Instalar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="f7460-126">Install hello app</span></span>
<span data-ttu-id="f7460-127">está disponible para la aplicación de Microsoft Authenticator Hello [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), y [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="f7460-127">hello Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-toohello-app"></a><span data-ttu-id="f7460-128">Agregar aplicación de cuentas toohello</span><span class="sxs-lookup"><span data-stu-id="f7460-128">Add accounts toohello app</span></span>
<span data-ttu-id="f7460-129">Para cada cuenta que desea que la aplicación de Microsoft Authenticator toohello tooadd, use uno de hello procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f7460-129">For each account that you want tooadd toohello Microsoft Authenticator app, use one of hello following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-toohello-app"></a><span data-ttu-id="f7460-130">Agregar una aplicación de toohello de cuentas de Microsoft personal</span><span class="sxs-lookup"><span data-stu-id="f7460-130">Add a personal Microsoft account toohello app</span></span>

<span data-ttu-id="f7460-131">Para una cuenta Microsoft personal (uno que use toosign en tooOutlook.com, Xbox, Skype, etc.), todo lo que tiene toodo es iniciar sesión en la cuenta de tooyour en la aplicación de Microsoft Authenticator hello.</span><span class="sxs-lookup"><span data-stu-id="f7460-131">For a personal Microsoft account (one that you use toosign in tooOutlook.com, Xbox, Skype, etc.), all you have toodo is sign in tooyour account in hello Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a><span data-ttu-id="f7460-132">Agregar un trabajo o escuela cuenta toohello aplicación mediante el escáner de código de hello QR</span><span class="sxs-lookup"><span data-stu-id="f7460-132">Add a work or school account toohello app using hello QR code scanner</span></span>
1. <span data-ttu-id="f7460-133">Vaya pantalla de configuración de comprobación de seguridad toohello.</span><span class="sxs-lookup"><span data-stu-id="f7460-133">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="f7460-134">Para obtener información acerca de cómo tooget toothis pantalla, consulte [cambiar la configuración de seguridad](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="f7460-134">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="f7460-135">Casilla de verificación Hola junto demasiado**aplicación Authenticator** , a continuación, seleccione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="f7460-135">Check hello box next too**Authenticator app** then select **Configure**.</span></span>

    ![botón configurar de Hello en pantalla de configuración de comprobación de seguridad de Hola](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="f7460-137">Aparecerá una pantalla con un código QR.</span><span class="sxs-lookup"><span data-stu-id="f7460-137">This brings up a screen with a QR code on it.</span></span>

    ![Pantalla que proporcione el código QR Hola](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="f7460-139">Aplicación de Microsoft Authenticator de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="f7460-139">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="f7460-140">En hello **cuentas** pantalla, seleccione  **+** y, a continuación, especifique que desea tooadd una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="f7460-140">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>
4. <span data-ttu-id="f7460-141">Utilice el código de hello QR de hello cámara tooscan y, a continuación, seleccione **realiza** pantalla de código de hello QR tooclose.</span><span class="sxs-lookup"><span data-stu-id="f7460-141">Use hello camera tooscan hello QR code, and then select **Done** tooclose hello QR code screen.</span></span>

    <span data-ttu-id="f7460-142">Si la cámara no funciona correctamente, puede [escribir código de hello QR y la dirección URL manualmente](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="f7460-142">If your camera is not working properly, you can [enter hello QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="f7460-143">Cuando la aplicación hello muestra el nombre de cuenta con un código de seis dígitos aparecen debajo de él, ya ha terminado.</span><span class="sxs-lookup"><span data-stu-id="f7460-143">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Pantalla Cuentas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a><span data-ttu-id="f7460-145">Agregar una aplicación de toohello de cuenta manualmente</span><span class="sxs-lookup"><span data-stu-id="f7460-145">Add an account toohello app manually</span></span>
1. <span data-ttu-id="f7460-146">Vaya pantalla de configuración de comprobación de seguridad toohello.</span><span class="sxs-lookup"><span data-stu-id="f7460-146">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="f7460-147">Para obtener información acerca de cómo tooget toothis pantalla, consulte [cambiar la configuración de seguridad](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="f7460-147">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="f7460-148">Seleccione **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="f7460-148">Select **Configure**.</span></span>

    ![botón configurar de Hello en pantalla de configuración de comprobación de seguridad de Hola](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="f7460-150">Aparecerá una pantalla con un código QR.</span><span class="sxs-lookup"><span data-stu-id="f7460-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="f7460-151">Tenga en cuenta el código de hello y la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="f7460-151">Note hello code and URL.</span></span>

    ![Pantalla que proporciona el código QR hello y la dirección URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="f7460-153">Aplicación de Microsoft Authenticator de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="f7460-153">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="f7460-154">En hello **cuentas** pantalla, seleccione  **+** y, a continuación, especifique que desea tooadd una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="f7460-154">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>

4. <span data-ttu-id="f7460-155">En el analizador de hello, seleccione **escribe código manualmente**.</span><span class="sxs-lookup"><span data-stu-id="f7460-155">In hello scanner, select **enter code manually**.</span></span>

    ![Pantalla para digitalizar un código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="f7460-157">Escriba código de hello y la URL de hello en los cuadros adecuados de hello en la aplicación hello, a continuación, seleccione **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="f7460-157">Enter hello code and hello URL in hello appropriate boxes in hello app, then select **Finish**.</span></span>

    ![Pantalla para escribir el código y la dirección URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="f7460-159">Cuando la aplicación hello muestra el nombre de cuenta con un código de seis dígitos aparecen debajo de él, ya ha terminado.</span><span class="sxs-lookup"><span data-stu-id="f7460-159">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Pantalla Cuentas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a><span data-ttu-id="f7460-161">Agregar una aplicación de toohello cuenta usa Touch ID</span><span class="sxs-lookup"><span data-stu-id="f7460-161">Add an account toohello app using Touch ID</span></span>
<span data-ttu-id="f7460-162">aplicación de Microsoft Authenticator Hello en iOS admite Touch Id.</span><span class="sxs-lookup"><span data-stu-id="f7460-162">hello Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="f7460-163">La autenticación multifactor Azure permite a las organizaciones toorequire un PIN para dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f7460-163">Azure Multi-Factor Authentication allows organizations toorequire a PIN for devices.</span></span> <span data-ttu-id="f7460-164">Con Touch ID, los usuarios de iOS no es necesario tooenter un PIN.</span><span class="sxs-lookup"><span data-stu-id="f7460-164">With Touch ID, iOS users don’t need tooenter a PIN.</span></span> <span data-ttu-id="f7460-165">En su lugar, pueden digitalizar su huella y seleccionar **Aprobar**.</span><span class="sxs-lookup"><span data-stu-id="f7460-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="f7460-166">Configurar Touch ID con Microsoft Authenticator es sencillo.</span><span class="sxs-lookup"><span data-stu-id="f7460-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="f7460-167">Un PIN supone un reto de comprobación normal.</span><span class="sxs-lookup"><span data-stu-id="f7460-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="f7460-168">Si el dispositivo es compatible con Touch ID, Microsoft Authenticator lo configura automáticamente para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="f7460-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Comprobación de la configuración de Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="f7460-170">Partir de ese punto en adelante, cuando esté necesario tooverify el inicio de sesión de, seleccione notificación de inserción de hello recibido y examinar su huella digital en lugar de escribir el código PIN.</span><span class="sxs-lookup"><span data-stu-id="f7460-170">From that point forward, when you're required tooverify your sign-in, you select hello received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Notificación push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a><span data-ttu-id="f7460-172">Usar una aplicación Hola al iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="f7460-172">Use hello app when you sign in</span></span>

<span data-ttu-id="f7460-173">Una vez que se agregue su cuenta de aplicación toohello, es posible que solicitadas toodo un toomake de comprobación de prueba que todo se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f7460-173">Once your account is added toohello app, you may be prompted toodo a test verification toomake sure everything was configured correctly.</span></span> <span data-ttu-id="f7460-174">Después de eso, habrá terminado.</span><span class="sxs-lookup"><span data-stu-id="f7460-174">After that, you're done!</span></span> <span data-ttu-id="f7460-175">No es necesario toodo nada hasta que hello próxima vez inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="f7460-175">You don't need toodo anything else until hello next time you sign in.</span></span>

<span data-ttu-id="f7460-176">Si elige toouse códigos de comprobación en la aplicación hello, iniciar toosee usarlas en la página de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7460-176">If you chose toouse verification codes in hello app, you start toosee them on hello home page.</span></span> <span data-ttu-id="f7460-177">Como cambian cada 30 segundos, siempre tendrá un código nuevo cuando lo necesite.</span><span class="sxs-lookup"><span data-stu-id="f7460-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="f7460-178">Pero no es necesario toodo nada con ellos hasta que inicie sesión y son tooenter solicitada un código de comprobación.</span><span class="sxs-lookup"><span data-stu-id="f7460-178">But you don't need toodo anything with them until you sign in and are prompted tooenter a verification code.</span></span>  
