### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="bac16-101">GRANT Mobile Engagement acceso tooyour clave de API GCM</span><span class="sxs-lookup"><span data-stu-id="bac16-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="bac16-102">notificaciones de inserción de tooallow Mobile Engagement toosend en su nombre, debe toogrant que tener acceso tooyour clave de API.</span><span class="sxs-lookup"><span data-stu-id="bac16-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="bac16-103">Esto se realiza mediante la configuración y escribir la clave en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="bac16-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="bac16-104">En el Portal clásico de Azure, asegúrese de que está en la aplicación de hello se usa para este proyecto y, a continuación, haga clic en hello **implique** situado en la parte inferior de hello:</span><span class="sxs-lookup"><span data-stu-id="bac16-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="bac16-105">A continuación, haga clic en hello **configuración** -> **inserción nativa** sección tooenter su clave de GCM:</span><span class="sxs-lookup"><span data-stu-id="bac16-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="bac16-106">Haga clic en hello **editar** icono delante del **clave de API** en hello **configuración GCM** sección tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="bac16-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="bac16-107">En el menú emergente de hello, Hola GCM servidor clave que obtuvo antes de pegar y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bac16-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="bac16-108"><a id="send"></a>Enviar una aplicación de tooyour de notificación</span><span class="sxs-lookup"><span data-stu-id="bac16-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="bac16-109">Se va a crear una campaña de notificación de inserción simple que envía una aplicación de tooour de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="bac16-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="bac16-110">Navegue toohello **ALCANZAR** ficha en el portal de interacción móvil.</span><span class="sxs-lookup"><span data-stu-id="bac16-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="bac16-111">Haga clic en **nuevo anuncio** toocreate la campaña de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="bac16-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="bac16-112">Configurar el primer campo de saludo de la campaña a través de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="bac16-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="bac16-113">a.</span><span class="sxs-lookup"><span data-stu-id="bac16-113">a.</span></span> <span data-ttu-id="bac16-114">Asigne un nombre a la campaña.</span><span class="sxs-lookup"><span data-stu-id="bac16-114">Name your campaign.</span></span>
   
    <span data-ttu-id="bac16-115">b.</span><span class="sxs-lookup"><span data-stu-id="bac16-115">b.</span></span> <span data-ttu-id="bac16-116">Seleccione hello **tipo de entrega** como *notificación del sistema -> Simple*: se trata de tipo de notificación de inserción de Android simple de Hola que ofrece un título y una pequeña línea de texto.</span><span class="sxs-lookup"><span data-stu-id="bac16-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="bac16-117">c.</span><span class="sxs-lookup"><span data-stu-id="bac16-117">c.</span></span> <span data-ttu-id="bac16-118">Seleccione **hora de entrega** como *cualquier momento* tooallow Hola aplicación tooreceive una notificación si se inicia la aplicación hello, o no.</span><span class="sxs-lookup"><span data-stu-id="bac16-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="bac16-119">d.</span><span class="sxs-lookup"><span data-stu-id="bac16-119">d.</span></span> <span data-ttu-id="bac16-120">Hola Hola de tipo de texto de notificación **título** que estará en negrita en la inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="bac16-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="bac16-121">e.</span><span class="sxs-lookup"><span data-stu-id="bac16-121">e.</span></span> <span data-ttu-id="bac16-122">Luego escriba su **mensaje**</span><span class="sxs-lookup"><span data-stu-id="bac16-122">Then type your **Message**</span></span>
4. <span data-ttu-id="bac16-123">Desplácese hacia abajo y en hello **contenido** sección, seleccione **solo notificación**.</span><span class="sxs-lookup"><span data-stu-id="bac16-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="bac16-124">Ha terminado la posible de campaña más básica de configuración Hola.</span><span class="sxs-lookup"><span data-stu-id="bac16-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="bac16-125">Ahora, desplácese hacia abajo en nuevo y haga clic en hello **crear** botón toosave la campaña.</span><span class="sxs-lookup"><span data-stu-id="bac16-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="bac16-126">Último paso: haga clic en **activar** tooactivate las notificaciones de inserción de toosend de campaña.</span><span class="sxs-lookup"><span data-stu-id="bac16-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

