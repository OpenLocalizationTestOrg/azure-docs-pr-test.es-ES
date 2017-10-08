---
title: aaaSign ins tras varios errores
description: "Un informe que indica los usuarios que han iniciado sesión correctamente después de varios intentos del inicio de sesión consecutivos."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="8a4f0-103">Inicios de sesión tras varios errores</span><span class="sxs-lookup"><span data-stu-id="8a4f0-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="8a4f0-104">Este informe indica los usuarios que han iniciado sesión correctamente después de varios intentos del inicio de sesión consecutivos.</span><span class="sxs-lookup"><span data-stu-id="8a4f0-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="8a4f0-105">Entre las posibles causas se incluyen las siguientes:</span><span class="sxs-lookup"><span data-stu-id="8a4f0-105">Possible causes include:</span></span>

* <span data-ttu-id="8a4f0-106">El usuario había olvidado su contraseña.</span><span class="sxs-lookup"><span data-stu-id="8a4f0-106">User had forgotten their password</span></span></li><li><span data-ttu-id="8a4f0-107">El usuario es víctima de Hola de una ataque por fuerza bruta de averiguación de contraseña correcta</span><span class="sxs-lookup"><span data-stu-id="8a4f0-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="8a4f0-108">Los resultados de este informe mostrará Hola número de intentos fallidos consecutivos de inicio de sesión realizados toohello anterior correcta inicio de sesión y Hola una marca de tiempo asociada a un inicio de sesión correcto primero.</span><span class="sxs-lookup"><span data-stu-id="8a4f0-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="8a4f0-109">**Configuración de informes**: puede configurar el número mínimo de Hola de inicio de sesión fallido consecutivo de intentos que deben realizarse antes de que puedan mostrarse en informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a4f0-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="8a4f0-110">Cuando realice cambios toothis establecerlo es toonote importante que estos cambios no estarán tooany aplicado existente error inicios que se muestran actualmente en el informe de sesión.</span><span class="sxs-lookup"><span data-stu-id="8a4f0-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="8a4f0-111">Sin embargo, estarán inicios de sesión futura tooall aplicada. Informe de cambios de toothis solo puede realizarse por los administradores con licencia.</span><span class="sxs-lookup"><span data-stu-id="8a4f0-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![Inicios de sesión tras varios errores](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

