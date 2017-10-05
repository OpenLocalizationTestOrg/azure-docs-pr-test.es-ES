---
title: "Introducción a la guía de prueba de concepto de Azure Active Directory | Microsoft Docs"
description: "Explorar e implementar rápidamente escenarios de administración de identidades y acceso"
services: active-directory
keywords: "azure active directory, guía, prueba de concepto, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a>Guía de prueba de concepto de Azure Active Directory: Introducción

En este artículo se proporcionan instrucciones para explorar las diferentes funcionalidades de Azure AD en una prueba de concepto (PoC). Los destinatarios de este documento son arquitectos de identidad, profesionales de TI e integradores de sistemas

## <a name="how-to-use-this-playbook"></a>Cómo usar esta guía

1. Use la sección [Tema](active-directory-playbook-ingredients.md#theme) y elija las áreas de interés según sus necesidades.  
2. Defina el ámbito de la prueba de concepto eligiendo los escenarios que se alineen con sus objetivos empresariales. Cuanto más breve, mejor. Se recomienda hacerlo tan breve y conciso como sea posible para transmitir el valor a las partes interesadas y, al mismo tiempo, minimizar su complejidad.  
3. Use la sección [Implementación](active-directory-playbook-implementation.md) para comprender los escenarios y lo significarían para su entorno. En cada escenario, se describe cómo configurar lo que llamamos [Bloques de creación](active-directory-playbook-building-blocks.md)) y cómo navegar por los escenarios. 
4. Cada bloque de creación explica los requisitos previos necesarios, así como un tiempo aproximado de realización. Esto puede ser de ayuda durante el proceso de planificación. 
5. En función de los puntos 1 al 3 anteriores, defina el [Entorno](active-directory-playbook-ingredients.md#environment) en el que se va a ejecutar. Le animamos a elegir en lo posible un entorno de producción para hacerse una idea de la experiencia para los usuarios. 
6. Si algunos de los requisitos plantea conflictos, puede utilizar la siguiente matriz de decisión 
   * Visualización del valor centrada en el tema  
   * Facilidad para preparar, configurar y ejecutar los escenarios 
   * Tiempo mínimo para ejecutar los escenarios de destino 
   * Tan próximo a un entorno de producción como sea posible dentro de las restricciones 

>[!NOTE]
> En este artículo, verá algunas aplicaciones específicas de terceros y productos que se mencionan como ejemplos para su comodidad. Azure AD admite miles de aplicaciones en su [Galería de aplicaciones](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) que puede usar en función de sus necesidades y entorno. 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]