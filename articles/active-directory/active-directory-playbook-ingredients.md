---
title: "aaaAzure ingredientes de guía de prueba de concepto de Active Directory | Documentos de Microsoft"
description: "Exploración e implementación rápida de escenarios de administración de identidades y acceso"
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
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Componentes de la guía de prueba de concepto de Azure Active Directory 

## <a name="theme"></a>Tema
Azure AD proporciona soluciones de identidad y acceso a través de varias áreas de empresa de Hola. Se clasificación escenarios Hola Hola siguientes áreas: 

* [Gran cantidad de aplicaciones, una identidad](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [Mejorar la seguridad](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [Escalable con autoservicio](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

Definir un tema tooframe ¡hello PoC ayuda a los esfuerzos de hello toofocus clara con los objetivos empresariales, que a menudo son desencadenadores de Hola de interés de hello en una prueba de concepto en primer lugar en Hola. 

## <a name="environment"></a>Environment

Es detalles de Hola toodetermine importante del entorno de Hola donde entregará Hola prueba de concepto. Lo ideal es que puede crear en él después de Hola que se ha completado la prueba de concepto. entorno de destino de Hello es crucial y debería encontrar el equilibrio adecuado de hello entre realizar, como real posible y la sobrecarga de Hola de restricciones o consideraciones adicionales. Hola entornos típicos para PoCs son:
* **Producción:** escenarios Hola se implementará en el entorno activo y ya implementado Microsoft Cloud services (solución de producción AD, Office 365, Azure AD inquilino/SSO). 
* **Pruebas de aceptación de usuario (UAT) o entorno de desarrollo:** Se dispone de una infraestructura de prueba (AD en paralelo y potencialmente un inquilino Azure AD, o una solución SSO) con datos de prueba similares a los de producción. Por lo general, entorno de prueba de Hola se comparte entre varios proyectos de empresa de Hola.

La mayoría de los escenarios en esta guía son aditivos por naturaleza. Como resultado, puede implementarse en el inquilino de producción de hello sin que afecte a los usuarios ajenos a Hola prueba de concepto. En este documento, se advertirá sobre los escenarios que pudieran tener efecto en todo el inquilino. En esos casos, conviene tooconsider un entorno no productivo. 


## <a name="target-users"></a>Usuarios de destino

Es importante toodetermine Hola destino conjunto de usuarios que actúan sobre escenarios de hello, especialmente cuando el entorno de hello es de producción o de prueba. Hola categorías de usuarios de destino para la prueba de concepto son:
* **Los usuarios del piloto:** funciones de trabajo de usuarios reales en el entorno de Hola que va a utilizar soluciones de hello con cuenta de hello que usan para su tooday día
* **Los usuarios de prueba:** probar las cuentas creadas en el entorno de Hola 

La mayoría de los escenarios de esta guía pueden realizarse con usuarios piloto. En este documento, se advertirá sobre consideraciones de los usuarios de destino si es necesario.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]