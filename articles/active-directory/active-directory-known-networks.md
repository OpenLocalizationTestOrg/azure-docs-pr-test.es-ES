---
title: "Redes conocidas en el Portal de Azure clásico | Microsoft Docs"
description: "Mediante la configuración de redes conocidas, puede evitar que direcciones IP que son propiedad de su organización estén incluidas en los informes \"Inicios de sesión desde varias ubicaciones geográficas\" e \"Inicios de sesión desde direcciones IP con actividad sospechosa\"."
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="78ebc-103">Redes conocidas</span><span class="sxs-lookup"><span data-stu-id="78ebc-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="78ebc-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="78ebc-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="78ebc-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78ebc-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="78ebc-106">Puede usar los informes de acceso y uso de Active Directory de Azure para proporcionar visibilidad sobre la integridad y la seguridad del directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="78ebc-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="78ebc-107">Con esta información, un administrador de directorios puede determinar mejor dónde puede haber posibles riesgos de seguridad de modo que pueda planear adecuadamente la mitigación de estos riesgos.</span><span class="sxs-lookup"><span data-stu-id="78ebc-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="78ebc-108">Es posible que los informes "*Inicios de sesión desde varias ubicaciones geográficas*" e "*Inicios de sesión desde direcciones IP con actividad sospechosa*" marquen incorrectamente las direcciones IP que en realidad son propiedad de su organización.</span><span class="sxs-lookup"><span data-stu-id="78ebc-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="78ebc-109">Por ejemplo, esto puede ocurrir cuando:</span><span class="sxs-lookup"><span data-stu-id="78ebc-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="78ebc-110">Un usuario de su oficina de Boston que ha iniciado sesión de forma remota en su centro de datos en San Francisco desencadena el informe "Inicios de sesión desde varias ubicaciones geográficas".</span><span class="sxs-lookup"><span data-stu-id="78ebc-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="78ebc-111">Un usuario de su organización que intenta iniciar sesión varias veces con una contraseña incorrecta desencadena el informe "Inicios de sesión desde direcciones IP con actividad sospechosa".</span><span class="sxs-lookup"><span data-stu-id="78ebc-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="78ebc-112">Para evitar estos casos de generación de informes de seguridad engañosos, debe agregar intervalos de direcciones IP conocidas a la lista de direcciones IP públicas de su organización.</span><span class="sxs-lookup"><span data-stu-id="78ebc-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="78ebc-113">Para ello, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78ebc-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="78ebc-114">Inicie sesión en el [Portal de administración de Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="78ebc-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="78ebc-115">En el panel izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78ebc-115">In the left pane, click **Active Directory**.</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="78ebc-117">En la pestaña **Directorio** , seleccione su directorio.</span><span class="sxs-lookup"><span data-stu-id="78ebc-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="78ebc-118">En el menú de la parte superior, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="78ebc-118">In the menu on the top, click **Configure**.</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="78ebc-120">En la pestaña Configurar, vaya a **los intervalos de direcciones IP públicos de las organizaciones**</span><span class="sxs-lookup"><span data-stu-id="78ebc-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="78ebc-122">Haga clic en **Agregar intervalos de direcciones IP conocidas**.</span><span class="sxs-lookup"><span data-stu-id="78ebc-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="78ebc-123">Agregue los intervalos de direcciones en el cuadro de diálogo que aparece y, luego, haga clic en el botón de comprobación cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="78ebc-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="78ebc-125">**Recursos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="78ebc-125">**Additional resources:**</span></span>

* [<span data-ttu-id="78ebc-126">Visualización de los informes de acceso y uso</span><span class="sxs-lookup"><span data-stu-id="78ebc-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="78ebc-127">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="78ebc-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="78ebc-128">Inicios de sesión desde varias ubicaciones geográficas</span><span class="sxs-lookup"><span data-stu-id="78ebc-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

