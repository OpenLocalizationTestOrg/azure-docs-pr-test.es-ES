### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="ae7fc-101">Conceder acceso tooyour insertar certificado tooMobile interacción</span><span class="sxs-lookup"><span data-stu-id="ae7fc-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="ae7fc-102">tooallow Mobile Engagement toosend notificaciones de inserción en su nombre, debe toogrant que tener acceso tooyour certificado.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="ae7fc-103">Esto se realiza mediante la configuración y especificar el certificado en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="ae7fc-104">Asegúrese de obtener el certificado. p12, tal y como se explica en la [documentación de Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="ae7fc-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="ae7fc-105">Navegue tooyour portal de interacción móvil.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="ae7fc-106">Asegúrese de se encuentra en hello correcto y, a continuación, haga clic en hello **implique** situado en la parte inferior de hello:</span><span class="sxs-lookup"><span data-stu-id="ae7fc-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="ae7fc-107">Haga clic en hello **configuración** página en el Portal de interacción.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="ae7fc-108">Desde allí, haga clic en hello **inserción nativa** sección tooupload su certificado p12:</span><span class="sxs-lookup"><span data-stu-id="ae7fc-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="ae7fc-109">Elija el certificado p12, cárguelo y escriba la contraseña:</span><span class="sxs-lookup"><span data-stu-id="ae7fc-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="ae7fc-110"><a id="send"></a>Enviar una aplicación de tooyour de notificación</span><span class="sxs-lookup"><span data-stu-id="ae7fc-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="ae7fc-111">Se creará una campaña de notificación de inserción simple que se va a enviar una aplicación de tooour de inserción:</span><span class="sxs-lookup"><span data-stu-id="ae7fc-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="ae7fc-112">Navegue toohello **alcanzar** ficha en el portal de interacción móvil.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="ae7fc-113">Haga clic en **nuevo anuncio** toocreate la campaña de inserción</span><span class="sxs-lookup"><span data-stu-id="ae7fc-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="ae7fc-114">El programa de instalación primeros campos de saludo de la campaña:</span><span class="sxs-lookup"><span data-stu-id="ae7fc-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="ae7fc-115">Proporcione un **Nombre** para la campaña.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="ae7fc-116">Seleccione hello **hora de entrega** como **fuera de la aplicación solo**: se trata de hello Apple push notificación tipo simple que incorpora algún texto.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="ae7fc-117">En el texto de la notificación de hello, escriba Hola primera **título** cuál es la primera línea de Hola de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="ae7fc-118">A continuación, escriba su **mensaje** que será la segunda línea de Hola</span><span class="sxs-lookup"><span data-stu-id="ae7fc-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="ae7fc-119">Desplácese hacia abajo y, en hello seleccione sección contenido **solo notificación**</span><span class="sxs-lookup"><span data-stu-id="ae7fc-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="ae7fc-120">Ha terminado la campaña más básica de Hola de configuración.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="ae7fc-121">Ahora, desplácese hacia abajo y haga clic en **crear** botón toosave la campaña de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="ae7fc-122">Por último - haga clic en **activar** toosend notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="ae7fc-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="ae7fc-123">Podrá recibir una notificación de hello en el dispositivo iOS en Centro de notificaciones de hello como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ae7fc-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="ae7fc-124">Si tienes un Apple Watch emparejado con este dispositivo iOS verá notificación hello en su Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="ae7fc-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

