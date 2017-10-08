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
# <a name="sign-ins-after-multiple-failures"></a>Inicios de sesión tras varios errores
Este informe indica los usuarios que han iniciado sesión correctamente después de varios intentos del inicio de sesión consecutivos. Entre las posibles causas se incluyen las siguientes:

* El usuario había olvidado su contraseña.</li><li>El usuario es víctima de Hola de una ataque por fuerza bruta de averiguación de contraseña correcta

Los resultados de este informe mostrará Hola número de intentos fallidos consecutivos de inicio de sesión realizados toohello anterior correcta inicio de sesión y Hola una marca de tiempo asociada a un inicio de sesión correcto primero.

**Configuración de informes**: puede configurar el número mínimo de Hola de inicio de sesión fallido consecutivo de intentos que deben realizarse antes de que puedan mostrarse en informes de Hola. Cuando realice cambios toothis establecerlo es toonote importante que estos cambios no estarán tooany aplicado existente error inicios que se muestran actualmente en el informe de sesión. Sin embargo, estarán inicios de sesión futura tooall aplicada. Informe de cambios de toothis solo puede realizarse por los administradores con licencia.

![Inicios de sesión tras varios errores](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

