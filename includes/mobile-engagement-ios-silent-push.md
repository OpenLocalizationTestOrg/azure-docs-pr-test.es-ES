> [!IMPORTANT]
> <span data-ttu-id="1834b-101">Para recibir notificaciones de inserción de Mobile Engagement, debe habilitar `Silent Remote Notifications` en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="1834b-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="1834b-102">Deberá agregar el valor remote-notification a la matriz UIBackgroundModes en el archivo Info.plist.</span><span class="sxs-lookup"><span data-stu-id="1834b-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="1834b-103">Abra el archivo `info.plist` del proyecto</span><span class="sxs-lookup"><span data-stu-id="1834b-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="1834b-104">Haga clic con el botón derecho en el elemento superior de la lista (`Information Property List`) y agregue una nueva fila</span><span class="sxs-lookup"><span data-stu-id="1834b-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="1834b-105">En la nueva fila, escriba `Required background modes`</span><span class="sxs-lookup"><span data-stu-id="1834b-105">In the new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="1834b-106">Haga clic en la flecha izquierda para expandir la fila</span><span class="sxs-lookup"><span data-stu-id="1834b-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="1834b-107">Agregue el siguiente valor al elemento 0 `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="1834b-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="1834b-108">Una vez realizado el cambio, info.plist XML debe contener la clave y el valor siguientes:</span><span class="sxs-lookup"><span data-stu-id="1834b-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="1834b-109">Si está usando **Xcode 7+** e **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="1834b-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="1834b-110">Habilite **Notificaciones push** en Destinos > Su nombre de destino > Capacidades.</span><span class="sxs-lookup"><span data-stu-id="1834b-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

