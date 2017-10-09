---
title: aaaUnderstanding DNS en la pila de Azure | Documentos de Microsoft
description: "Información acerca de las características y funcionalidades de DNS en Azure Stack"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a>Presentación de iDNS para Azure Stack
================================

IDN es una característica de pila de Azure que permite tooresolve de nombres DNS externos (por ejemplo, http://www.bing.com).
También permite nombres de red virtual interna tooregister. Al hacerlo, puede resolver las máquinas virtuales en hello misma red virtual por nombre en lugar de IP de direcciones, sin necesidad de entradas de servidor DNS personalizadas tooprovide.

Es algo con lo que siempre ha contado Azure, pero ahora también está disponible en Windows Server 2016 y Azure Stack.

## <a name="what-does-idns-do"></a>¿Para qué sirve iDNS?
Con IDN en la pila de Azure, obtendrá Hola siguientes capacidades, sin necesidad de entradas de servidor DNS personalizadas toospecify.

* Servicios de resolución de nombres Compartir los servicios de resolución de nombres DNS compartidos para las cargas de trabajo del inquilino.
* Servicio DNS autoritativo para la resolución de nombres y el registro DNS en la red virtual del inquilino de Hola.
* Servicio DNS recursivo para la resolución de los nombres de Internet de las máquinas virtuales de los inquilinos. Los inquilinos ya no necesitan toospecify DNS entradas tooresolve Internet nombres personalizados (por ejemplo, www.bing.com).

Si lo desea, puede traer su propio DNS y utilizar servidores DNS personalizados. Pero ahora, si simplemente desea nombres de DNS de Internet pueda tooresolve toobe y ser capaz de tooconnect tooother máquinas virtuales Hola misma red virtual, no necesita toospecify nada y funcionarán correctamente.

## <a name="what-does-idns-not-do"></a>¿Qué es lo que iDNS no hace?
Qué IDN no permite toodo es crear un registro DNS para un nombre que se pueda resolver desde la red virtual externa Hola.

En Azure, tiene la opción de Hola de especificar una etiqueta de nombre DNS que se puede asociar con una dirección IP pública. Puede elegir la etiqueta de hello (prefijo), pero Azure elige sufijo hello, que se basa en la región de hello en el que crear la dirección IP pública Hola.

![Captura de pantalla de etiqueta de nombre DNS](media/azure-stack-understanding-dns-in-tp2/image3.png)

En la imagen anterior de hello, Azure creará un registro "A" en DNS para la etiqueta de nombre DNS de hello especificado en la zona de hello **westus.cloudapp.azure.com**. El sufijo hello y prefijo juntas componen un dominio nombre completo (FQDN) que se puede resolver desde cualquier lugar en Hola Internet pública.

Azure pila solo admite IDN para el registro de nombres interna, por lo que no es posible Hola después.

* Crear un registro DNS en una zona DNS hospedada existente (por ejemplo, local.azurestack.external).
* Crear una zona DNS (como Contoso.com).
* Crear un registro en su propia zona DNS personalizada.
* Admite la compra de Hola de nombres de dominio.

