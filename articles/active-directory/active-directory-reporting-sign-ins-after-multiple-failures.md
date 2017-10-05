---
title: "Inicios de sesión tras varios errores"
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
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="74f83-103">Inicios de sesión tras varios errores</span><span class="sxs-lookup"><span data-stu-id="74f83-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="74f83-104">Este informe indica los usuarios que han iniciado sesión correctamente después de varios intentos del inicio de sesión consecutivos.</span><span class="sxs-lookup"><span data-stu-id="74f83-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="74f83-105">Entre las posibles causas se incluyen las siguientes:</span><span class="sxs-lookup"><span data-stu-id="74f83-105">Possible causes include:</span></span>

* <span data-ttu-id="74f83-106">El usuario había olvidado su contraseña.</span><span class="sxs-lookup"><span data-stu-id="74f83-106">User had forgotten their password</span></span></li><li><span data-ttu-id="74f83-107">El usuario es víctima de un ataque por fuerza bruta de averiguación de contraseñas que ha logrado su objetivo.</span><span class="sxs-lookup"><span data-stu-id="74f83-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="74f83-108">Los resultados de este informe le mostrarán el número de intentos de inicio de sesión erróneos consecutivos realizados antes del inicio de sesión correcto, así como una marca de tiempo asociada con el primer inicio de sesión correcto.</span><span class="sxs-lookup"><span data-stu-id="74f83-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="74f83-109">**Configuración del informe**: puede configurar el número mínimo de intentos de inicio de sesión erróneos consecutivos que se deben producir para que aparezcan en el informe.</span><span class="sxs-lookup"><span data-stu-id="74f83-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="74f83-110">Al realizar cambios en esta configuración, es importante tener en cuenta que estos cambios no se aplicarán a cualquier inicio de sesión erróneo existente que se muestra actualmente en el informe existente.</span><span class="sxs-lookup"><span data-stu-id="74f83-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="74f83-111">Sin embargo, se aplicarán a todos los inicios de sesión futuros.</span><span class="sxs-lookup"><span data-stu-id="74f83-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="74f83-112">Los cambios realizados en este informe solo los pueden llevar a cabo los administradores con licencia.</span><span class="sxs-lookup"><span data-stu-id="74f83-112">Changes to this report can only be made by licensed admins.</span></span>

![Inicios de sesión tras varios errores](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

