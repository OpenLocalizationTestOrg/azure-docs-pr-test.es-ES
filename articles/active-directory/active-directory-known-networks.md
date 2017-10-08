---
title: "Redes aaaKnown Hola portal de Azure clásico | Documentos de Microsoft"
description: "Al configurar redes conocidas, puede evitar tener direcciones IP que pertenecen a su organización incluido en hello inicios de sesión desde varias zonas geográficas y los inicios de sesión desde direcciones IP con informes de actividad sospechosa."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="ae12c-103">Redes conocidas</span><span class="sxs-lookup"><span data-stu-id="ae12c-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae12c-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="ae12c-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="ae12c-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ae12c-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="ae12c-106">Puede usar el acceso de Active Directory de Azure y visibilidad de toogain de informes de uso de integridad de Hola y seguridad del directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="ae12c-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="ae12c-107">Con esta información, administradores de directorios pueden determinar mejor dónde puede haber posibles riesgos de seguridad para que se pueden planificar adecuadamente toomitigate esos riesgos.</span><span class="sxs-lookup"><span data-stu-id="ae12c-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="ae12c-108">Es posible que Hola "*inicios de sesión desde varias zonas geográficas*"y"*inicios de sesión desde direcciones IP con actividad sospechosa*" informes marca incorrectamente las direcciones IP que realmente pertenecen a su organización.</span><span class="sxs-lookup"><span data-stu-id="ae12c-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="ae12c-109">Por ejemplo, esto puede ocurrir cuando:</span><span class="sxs-lookup"><span data-stu-id="ae12c-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="ae12c-110">Ha iniciado sesión un usuario en la oficina de Boston en forma remota tooyour centro de datos en San Francisco desencadenadores Hola informes "Inicios de sesión desde varias zonas geográficas"</span><span class="sxs-lookup"><span data-stu-id="ae12c-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="ae12c-111">Intenta usar un usuario de su organización toosign en varias veces una contraseña incorrecta desencadenadores donde aparece hello con informes de "Inicios de sesión desde direcciones IP con actividad sospechosa"</span><span class="sxs-lookup"><span data-stu-id="ae12c-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="ae12c-112">informa de estos casos de la seguridad puede inducir a error de generación de tooprevent, debe agregar conocidos intervalos toohello lista de direcciones IP la dirección IP pública de su organización.</span><span class="sxs-lookup"><span data-stu-id="ae12c-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="ae12c-113">intervalos de tooadd la dirección IP pública de su organización, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ae12c-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="ae12c-114">Inicio de sesión toohello [portal de administración de Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ae12c-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="ae12c-115">En el panel izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae12c-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="ae12c-117">Hola **Directory** ficha, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="ae12c-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="ae12c-118">En el menú de hello en la parte superior de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="ae12c-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="ae12c-120">En la ficha configurar de hello, vaya demasiado**los intervalos de direcciones IP públicos de las organizaciones**</span><span class="sxs-lookup"><span data-stu-id="ae12c-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="ae12c-122">Haga clic en **Agregar intervalos de direcciones IP conocidas**.</span><span class="sxs-lookup"><span data-stu-id="ae12c-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="ae12c-123">Agregar los intervalos de direcciones en el cuadro de diálogo de Hola que aparece y, a continuación, haga clic en botón de comprobación de hello cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="ae12c-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="ae12c-125">**Recursos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="ae12c-125">**Additional resources:**</span></span>

* [<span data-ttu-id="ae12c-126">Visualización de los informes de acceso y uso</span><span class="sxs-lookup"><span data-stu-id="ae12c-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="ae12c-127">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="ae12c-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="ae12c-128">Inicios de sesión desde varias ubicaciones geográficas</span><span class="sxs-lookup"><span data-stu-id="ae12c-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

