---
title: Utilizar emoticonos Emoji dentro de Azure Mobile Engagement
description: Uso de emoticonos Emoji dentro de las notificaciones push
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="82232-103">Uso de emoticonos Emoji dentro de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="82232-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="82232-104">Puede incluir emoticonos Emoji en las notificaciones de inserción en unos cuantos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="82232-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="82232-105">En primer lugar, debe encontrar el Emoji que desea enviar en el mensaje.</span><span class="sxs-lookup"><span data-stu-id="82232-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="82232-106">Asegúrese de que el Emoji que está seleccionando se admitirá en el dispositivo de destino, ya que los fabricantes de dispositivos tardan algún tiempo en agregar Emojis aprobados recientemente a las plataformas de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="82232-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="82232-107">En **Windows** puede navegar a esta [vínculo](http://apps.timwhitlock.info/emoji/tables/unicode) y copiar el icono “Native”.</span><span class="sxs-lookup"><span data-stu-id="82232-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="82232-108">En **Mac** puede encontrar los Emojis en la aplicación del diccionario en Edición -> Emoji y símbolos.</span><span class="sxs-lookup"><span data-stu-id="82232-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="82232-109">Ahora vaya a la pestaña **Reach** en el portal de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="82232-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="82232-110">Seleccione el tipo de notificación push (anuncio, encuestas, etc.).</span><span class="sxs-lookup"><span data-stu-id="82232-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="82232-111">En este ejemplo, elegimos una inserción de anuncio.</span><span class="sxs-lookup"><span data-stu-id="82232-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="82232-112">Especifique los distintos campos de la notificación hasta que llegue al texto de la notificación.</span><span class="sxs-lookup"><span data-stu-id="82232-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="82232-113">Aquí es donde agregará el emoticono Emoji.</span><span class="sxs-lookup"><span data-stu-id="82232-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="82232-114">Puede colocarlo en el título, en el mensaje o en ambos.</span><span class="sxs-lookup"><span data-stu-id="82232-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="82232-115">Debe arrastrar y soltar o copiar el Emoji que encontrará en las ubicaciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="82232-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="82232-116">Complete los demás campos de la notificación y guárdela.</span><span class="sxs-lookup"><span data-stu-id="82232-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="82232-117">Al ejecutar una prueba o activar el anuncio, verá una notificación con el emoticono tal y como lo especificó.</span><span class="sxs-lookup"><span data-stu-id="82232-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="82232-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="82232-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

