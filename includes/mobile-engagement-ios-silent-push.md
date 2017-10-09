> [!IMPORTANT]
> <span data-ttu-id="a3459-101">tooreceive notificaciones de inserción de Mobile Engagement, necesita tooenable `Silent Remote Notifications` en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3459-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="a3459-102">Necesitará tooadd Hola valor remoto notificación toohello UIBackgroundModes matriz en el archivo Info.plist.</span><span class="sxs-lookup"><span data-stu-id="a3459-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="a3459-103">Abra `info.plist` archivo de proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="a3459-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="a3459-104">Haga clic en el elemento superior de hello en lista de hello (`Information Property List`) y agregue una nueva fila</span><span class="sxs-lookup"><span data-stu-id="a3459-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="a3459-105">Hola escriba nueva fila`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="a3459-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="a3459-106">Haga clic en la fila de hello flecha izquierda tooexpand Hola</span><span class="sxs-lookup"><span data-stu-id="a3459-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="a3459-107">Agregar Hola sigue valor toohello elemento 0`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="a3459-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="a3459-108">Una vez cambiar hello, info.plist Hola XML debe contener Hola después de la clave y valor:</span><span class="sxs-lookup"><span data-stu-id="a3459-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="a3459-109">Si está usando **Xcode 7+** e **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="a3459-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="a3459-110">Habilite **Notificaciones push** en Destinos > Su nombre de destino > Capacidades.</span><span class="sxs-lookup"><span data-stu-id="a3459-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

