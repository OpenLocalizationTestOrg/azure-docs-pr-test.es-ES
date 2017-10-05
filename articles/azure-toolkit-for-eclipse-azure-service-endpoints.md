---
title: "Puntos de conexión de servicio de Azure"
description: "Describe la configuración del punto de conexión del servicio de Azure en kit de herramientas de Azure para Eclipse."
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
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="bcf2f-103">Puntos de conexión de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="bcf2f-103">Azure Service Endpoints</span></span>
<span data-ttu-id="bcf2f-104">Los puntos de conexión de servicio determinan si la aplicación se implementa y se administra en la plataforma global de Azure, es operada en Azure por medio de 21Vianet en China o en una plataforma privada de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="bcf2f-105">El cuadro de diálogo **Extremos de servicio** permite especificar qué puntos de conexión de servicio quiere usar.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="bcf2f-106">Para abrir el cuadro de diálogo **Extremos de servicio**, en Eclipse, haga clic en **Ventana**, en **Preferencias**, expanda **Azure** y luego haga clic en **Extremos de servicio**.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="bcf2f-107">Al establecer el campo **Conjunto activo** se determinan qué puntos de conexión de servicio de Azure se usarán para los proyectos de Azure en el área de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="bcf2f-108">Lo siguiente muestra el cuadro de diálogo **Extremos de servicio** .</span><span class="sxs-lookup"><span data-stu-id="bcf2f-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="bcf2f-109">Para establecer los puntos de conexión del servicio</span><span class="sxs-lookup"><span data-stu-id="bcf2f-109">To set the service endpoints</span></span>
<span data-ttu-id="bcf2f-110">En el cuadro de diálogo **Extremos de servicio** , realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="bcf2f-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="bcf2f-111">Si quiere usar la plataforma de Azure global, en la lista desplegable **Conjunto activo**, seleccione **windowsazure.com** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="bcf2f-112">Si quiere usar Azure operado por 21Vianet en China, en la lista desplegable **Conjunto activo**, seleccione **windowsazure.cn (China)** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="bcf2f-113">Si quiere usar una plataforma de Azure privada:</span><span class="sxs-lookup"><span data-stu-id="bcf2f-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="bcf2f-114">Haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="bcf2f-115">Se abre un cuadro de diálogo en el que se le informa de que se cerrará el cuadro de diálogo **Extremos de servicio** y de que se abrirá el archivo de conjuntos de preferencias.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="bcf2f-116">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-116">Click **OK**.</span></span>

  3. <span data-ttu-id="bcf2f-117">En el archivo preferencesets.xml, cree un nuevo elemento `preferenceset` .</span><span class="sxs-lookup"><span data-stu-id="bcf2f-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="bcf2f-118">Para este elemento nuevo, cree los atributos `name`, `blob`, `management`, `portalURL` y `publishsettings` y agregue valores para ellos que se correspondan a su plataforma de Azure privada.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="bcf2f-119">Puede usar los valores ofrecidos para los elementos `preferenceset` existentes como plantillas.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="bcf2f-120">**Nota**: el valor usado para el atributo `blob` debe contener el texto "blob" en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="bcf2f-121">Guarde y cierre preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="bcf2f-122">Vuelva a abrir el cuadro de diálogo **Extremos de servicio** .</span><span class="sxs-lookup"><span data-stu-id="bcf2f-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="bcf2f-123">En la lista desplegable **Conjunto activo**, seleccione el conjunto activo que ha creado y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="bcf2f-124">Cuando haya creado su elemento `preferenceset` de la plataforma de Azure privada, para cambiar sus valores asignados, haga clic en el botón **Editar** del cuadro de diálogo **Punto de conexión de servicios**.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="bcf2f-125">También puede crear varios elementos `preferenceset` de la plataforma de Azure privada, si así lo desea.</span><span class="sxs-lookup"><span data-stu-id="bcf2f-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="bcf2f-126">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="bcf2f-126">See Also</span></span>
<span data-ttu-id="bcf2f-127">[kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bcf2f-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="bcf2f-128">[Instalación del Kit de herramientas de Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bcf2f-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="bcf2f-129">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bcf2f-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="bcf2f-130">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="bcf2f-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
