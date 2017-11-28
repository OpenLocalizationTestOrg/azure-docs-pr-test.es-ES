
1. <span data-ttu-id="2c87d-101">En [Azure Portal](https://portal.azure.com/), haga clic en **Examinar todo** > **App Services** y finalmente en el back-end de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="2c87d-101">In the [Azure portal](https://portal.azure.com/), click **Browse All** > **App Services**, and then click your Mobile Apps back end.</span></span> <span data-ttu-id="2c87d-102">En **Configuración**, haga clic en **App Service Push** y, después, en el nombre del centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2c87d-102">Under **Settings**, click **App Service Push**, and then click your notification hub name.</span></span>
2. <span data-ttu-id="2c87d-103">Vaya a **Google (GCM)**, escriba el valor de **Clave de servidor** que obtuvo de Firebase en el procedimiento anterior y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2c87d-103">Go to **Google (GCM)**, enter the **Server Key** value that you obtained from Firebase in the previous procedure, and then click **Save**.</span></span>

    ![Establezca la clave de API de GCM en el portal](./media/app-service-mobile-android-configure-push/mobile-push-api-key.png)

<span data-ttu-id="2c87d-105">El back-end de·Mobile Apps ahora está configurado para usar Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="2c87d-105">The Mobile Apps back end is now configured to use Firebase Cloud Messaging.</span></span> <span data-ttu-id="2c87d-106">Esto permite enviar notificaciones push a la aplicación que se ejecuta en un dispositivo Android mediante el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2c87d-106">This enables you to send push notifications to your app running on an Android device, by using the notification hub.</span></span>

<!-- URLs. -->


<!-- images -->
