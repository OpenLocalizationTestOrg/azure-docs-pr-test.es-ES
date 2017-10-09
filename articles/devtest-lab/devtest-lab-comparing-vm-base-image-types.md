---
title: "aaaComparing imágenes personalizadas y las fórmulas en los laboratorios de desarrollo y pruebas | Documentos de Microsoft"
description: "Obtenga información sobre las diferencias de hello entre imágenes personalizadas y las fórmulas como bases de máquina virtual para que pueda decidir que mejor se adapte a su entorno."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>Comparación de imágenes personalizadas y fórmulas en DevTest Labs
Se pueden usar [imágenes personalizadas](devtest-lab-create-template.md) y [fórmulas](devtest-lab-manage-formulas.md) como base para las [nuevas máquinas virtuales creadas](devtest-lab-add-vm-with-artifacts.md). Sin embargo, distinción de clave de hello entre imágenes personalizadas y las fórmulas es que una imagen personalizada es simplemente una imagen basada en un disco duro virtual, mientras que una fórmula no es una imagen basada en un disco duro virtual *además* preconfigurado configuración - como el tamaño de máquina virtual, red virtual, subred y artefactos. Estos valores preconfigurados se configuran con los valores predeterminados que se pueden invalidar en tiempo de Hola de creación de máquinas virtuales. Este artículo explica algunas de las ventajas de hello (los profesionales de TI) y desventajas (cons) toousing imágenes personalizadas frente al uso de las fórmulas.

## <a name="custom-image-pros-and-cons"></a>Ventajas y desventajas de las imágenes personalizadas
Imágenes personalizadas proporcionan una toocreate de manera estática, inmutable máquinas virtuales de un entorno deseado. 

**Ventajas**

* Aprovisionamiento de una imagen personalizada de VM es rápido cuando no cambie nada después de hello que VM se active de imagen de Hola. En otras palabras, no hay ningún tooapply de configuración como imagen personalizada hello es simplemente una imagen sin configuración. 
* Las máquinas virtuales creadas a partir de una sola imagen personalizada son idénticas.

**Desventajas**

* Si necesita tooupdate algún aspecto de la imagen personalizada de hello, se debe recrear la imagen de Hola.  

## <a name="formula-pros-and-cons"></a>Ventajas y desventajas de las fórmulas
Las fórmulas proporcionan un toocreate de manera dinámica las máquinas virtuales de configuración de hello deseado.

**Ventajas**

* Se pueden capturar cambios en el entorno de hello en marcha de Hola a través de artefactos. Por ejemplo, si desea que una máquina virtual que se instala con bits más recientes de hello en la canalización de versiones o dar de alta código más reciente de Hola desde el repositorio, puede especificar simplemente un artefacto que implementa los bits más recientes de Hola o se da de alta código más reciente de hello en fórmula Hola junto con un imagen base del destino. Siempre que esta fórmula se usa toocreate las máquinas virtuales, bits/código más reciente de hello son implementado/dado de alta toohello máquina virtual. 
* Las fórmulas pueden definir la configuración predeterminada que las imágenes personalizadas no pueden proporcionar; por ejemplo, tamaños de máquina virtual y configuración de red virtual. 
* configuración de Hello guardada en una fórmula se muestra como valores predeterminados, pero puede modificarse cuando se crea la VM de Hola. 

**Desventajas**

* La creación de una máquina virtual a partir de una fórmula puede tardar más que la creación de una máquina virtual a partir de una imagen personalizada.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Entradas blogs relacionadas
* [Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Pasos siguientes
- [Preguntas frecuentes sobre DevTest Labs](devtest-lab-faq.md)