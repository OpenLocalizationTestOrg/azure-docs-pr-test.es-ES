---
title: aaaTroubleshoot RBAC de Azure | Documentos de Microsoft
description: Obtenga ayuda para los problemas o dudas que le surjan relativos a los recursos del control de acceso basado en roles.
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>Solución de problemas del control de acceso basado en rol

En este artículo de documento preguntas más frecuentes sobre los derechos de acceso específicos de Hola que se conceden con roles, para que sepa qué tooexpect cuando usan Hola roles Hola portal de Azure y se puede solucionar problemas de acceso. Estos tres roles abarcan todos los tipos de recursos:

* Propietario  
* Colaborador  
* Lector  

Los propietarios y colaboradores tienen acceso total toohello administración de experiencia, pero un colaborador no puede conceder acceso tooother usuarios o grupos. Puede ser un poco más interesante con rol de lector de hello, por lo es donde se pasará algún tiempo. Vea hello [artículo iniciada por get de Control de acceso basado en roles](role-based-access-control-configure.md) para obtener más información sobre cómo tener acceso toogrant.

## <a name="app-service-workloads"></a>Cargas de trabajo del Servicio de aplicaciones
### <a name="write-access-capabilities"></a>Funcionalidades de acceso de escritura
Si se concede una acceso de solo lectura de usuario tooa web única aplicación, se deshabilitan algunas características que no cabría esperar. Hola después de capacidades de administración requiere **escribir** acceder a la aplicación web de tooa (colaborador o propietario) y no están disponibles en cualquier escenario de solo lectura.

* Comandos (p. ej., iniciar, parar, etc.)
* Cambiar opciones, como la configuración general, opciones de escala, opciones de copia de seguridad y opciones de supervisión
* Acceder a las credenciales de publicación y otros secretos, como opciones de aplicaciones y cadenas de conexión
* Registros de streaming
* Configuración de registros de diagnóstico
* Consola (símbolo del sistema)
* Implementaciones activas y recientes (para implementaciones git continuas locales)
* Gasto estimado
* Pruebas web
* Red virtual (solo visible tooa lector si ya ha configurado una red virtual por un usuario con acceso de escritura).

Si no se puede obtener acceso a cualquiera de estos iconos, deberá tooask el administrador para la aplicación web de colaborador acceso toohello.

### <a name="dealing-with-related-resources"></a>Tratar con recursos relacionados
Las aplicaciones Web se ve complicadas por presencia de Hola de solo unos pocos recursos diferentes que interacción. Este es un grupo de recursos típico con un par de sitios web:

![Grupo de recursos de aplicación web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

Como resultado, si concede a alguien acceso toojust hello web app, gran parte de la funcionalidad de hello en la hoja de sitio Web de Hola Hola portal de Azure está deshabilitada.

Estos elementos requieren **escribir** acceso toohello **plan de servicio de aplicaciones** que corresponde el sitio Web de tooyour:  

* Aplicación web de Hola de visualización del plan de tarifa (gratuito o estándar)  
* Configuración de escala (número de instancias, tamaño de la máquina virtual y configuración de escala automática).  
* Cuotas (almacenamiento, ancho de banda y CPU).  

Estos elementos requieren **escribir** toohello acceso todo **grupo de recursos** que contiene el sitio Web:  

* Certificados SSL y enlaces (certificados SSL pueden compartirse entre los sitios de hello mismo grupo de recursos y la ubicación geográfica)  
* Las reglas de alertas  
* Opciones de escala automática  
* Componentes de Application Insights  
* Pruebas web  

## <a name="virtual-machine-workloads"></a>Cargas de trabajo de máquina virtual
Mucho al igual que con las aplicaciones web, algunas características de hoja de la máquina virtual de hello requieren una máquina virtual de acceso de escritura toohello o tooother recursos en grupo de recursos de Hola.

Máquinas virtuales son nombres tooDomain relacionados, redes virtuales, cuentas de almacenamiento y las reglas de alerta.

Estos elementos requieren **escribir** acceso toohello **Máquina Virtual**:

* Puntos de conexión  
* Direcciones IP  
* Discos  
* Extensiones  

Se requiere el **escribir** Hola de acceso tooboth **Máquina Virtual**, hello y **grupo de recursos** (junto con el nombre de dominio de Hola) que se encuentre en:  

* El conjunto de disponibilidad  
* El conjunto de carga equilibrada  
* Las reglas de alertas  

Si no se puede obtener acceso a cualquiera de estos iconos, pida al administrador para el grupo de recursos de toohello de acceso de colaborador.

## <a name="see-more"></a>Ver más
* [Control de acceso basado en roles](role-based-access-control-configure.md): comience a usar RBAC en hello portal de Azure.
* [Funciones integradas](role-based-access-built-in-roles.md): obtener detalles acerca de los roles de Hola que vienen en RBAC.
* [Roles personalizados en Azure RBAC](role-based-access-control-custom-roles.md): Obtenga información acerca de cómo toocreate roles personalizados toofit sus necesidades de acceso.
* [Creación de un informe del historial de cambios de acceso](role-based-access-control-access-change-history-report.md): seguimiento del cambio de asignaciones de roles en RBAC.

