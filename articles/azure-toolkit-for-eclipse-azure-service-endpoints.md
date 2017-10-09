---
title: aaaAzure los extremos de servicio
description: "Describe la configuración de extremo de servicio de Azure de hello en hello Azure Toolkit for Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="c0617-103">Puntos de conexión de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="c0617-103">Azure Service Endpoints</span></span>
<span data-ttu-id="c0617-104">Los puntos de conexión de servicio de Azure determinan que si la aplicación está implementada tooand administrado por la plataforma global de Azure hello, Azure operado por 21Vianet en China o una privada plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="c0617-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="c0617-105">Hola **los extremos de servicio** cuadro de diálogo permite toospecify que desea toouse de los extremos del servicio.</span><span class="sxs-lookup"><span data-stu-id="c0617-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="c0617-106">Hola tooopen **los extremos de servicio** cuadro de diálogo, en Eclipse, haga clic en **ventana**, haga clic en **preferencias**, expanda **Azure**y, a continuación, haga clic en **Los extremos del servicio**.</span><span class="sxs-lookup"><span data-stu-id="c0617-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="c0617-107">Hola configuración **conjunto Active** campo determina qué servicio de Azure extremos se utilizarán para hello Azure proyectos en el área de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="c0617-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="c0617-108">siguiente Hello muestra hello **los extremos de servicio** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c0617-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="c0617-109">extremos de servicio de hello tooset</span><span class="sxs-lookup"><span data-stu-id="c0617-109">tooset hello service endpoints</span></span>
<span data-ttu-id="c0617-110">Hola **los extremos de servicio** cuadro de diálogo, realice una de hello siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="c0617-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="c0617-111">Si desea toouse Hola plataforma global de Azure, de hello **conjunto Active** lista desplegable, seleccione **windowsazure.com** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c0617-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="c0617-112">Si desea toouse Azure operado por 21Vianet en China, de hello **conjunto Active** lista desplegable, seleccione **windowsazure.cn (China)** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c0617-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="c0617-113">Si desea que toouse una plataforma de Azure privada:</span><span class="sxs-lookup"><span data-stu-id="c0617-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="c0617-114">Haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="c0617-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="c0617-115">Se abre un cuadro de diálogo, que le informa de que hello **los extremos de servicio** cuadro de diálogo se cerrará y se abrirá el archivo de conjuntos de preferencias de hello.</span><span class="sxs-lookup"><span data-stu-id="c0617-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="c0617-116">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c0617-116">Click **OK**.</span></span>

  3. <span data-ttu-id="c0617-117">En el archivo de hello preferencesets.xml, cree un nuevo `preferenceset` elemento.</span><span class="sxs-lookup"><span data-stu-id="c0617-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="c0617-118">Para este nuevo elemento, crear `name`, `blob`, `management`, `portalURL` y `publishsettings` atributos y agrégueles valores correspondientes de la plataforma de Azure privada tooyour.</span><span class="sxs-lookup"><span data-stu-id="c0617-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="c0617-119">Puede utilizar valores de hello proporcionados Hola existentes `preferenceset` elementos como plantillas.</span><span class="sxs-lookup"><span data-stu-id="c0617-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="c0617-120">**Tenga en cuenta**: Hola valor utilizado para hello `blob` atributo debe contener texto hello "blob" en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0617-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="c0617-121">Guarde y cierre preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="c0617-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="c0617-122">Vuelva a abrir hello **los extremos de servicio** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c0617-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="c0617-123">De hello **conjunto Active** lista desplegable, seleccione Hola activo establecido que creó y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c0617-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="c0617-124">Una vez que ha creado su plataforma de Azure privada `preferenceset` elemento, puede cambiar Hola valores asignados tooit haciendo clic en hello **editar** botón en hello **punto de conexión de servicios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c0617-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="c0617-125">También puede crear varios elementos `preferenceset` de la plataforma de Azure privada, si así lo desea.</span><span class="sxs-lookup"><span data-stu-id="c0617-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="c0617-126">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c0617-126">See Also</span></span>
<span data-ttu-id="c0617-127">[kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c0617-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="c0617-128">[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c0617-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="c0617-129">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c0617-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="c0617-130">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="c0617-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
