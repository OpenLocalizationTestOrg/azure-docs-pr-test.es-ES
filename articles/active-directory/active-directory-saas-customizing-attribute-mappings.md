---
title: aaaCustomizing asignaciones de atributos de AD de Azure | Documentos de Microsoft
description: "Averigüe qué asignaciones de atributos para las aplicaciones SaaS en Azure Active Directory cómo puede modificarlas tooaddress su empresa necesita."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="50d19-103">Personalización de asignaciones de atributos de aprovisionamiento de usuarios para aplicaciones SaaS en Azure Active Directory de usuarios</span><span class="sxs-lookup"><span data-stu-id="50d19-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="50d19-104">Microsoft Azure AD proporciona compatibilidad con aplicaciones de SaaS toothird terceros como Salesforce, Google Apps y otros de aprovisionamiento de usuarios.</span><span class="sxs-lookup"><span data-stu-id="50d19-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="50d19-105">Si tiene usuarios de aprovisionamiento de una aplicación de SaaS de terceros habilitada, Hola Portal de administración de Azure controla sus valores de atributo en forma de una configuración conocida como "asignación de atributos".</span><span class="sxs-lookup"><span data-stu-id="50d19-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="50d19-106">Hay un conjunto preconfigurado de asignaciones de atributos entre los objetos de usuario de Azure AD y los objetos de usuario de cada aplicación SaaS.</span><span class="sxs-lookup"><span data-stu-id="50d19-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="50d19-107">Algunas aplicaciones administran otros tipos de objetos, como grupos o contactos.</span><span class="sxs-lookup"><span data-stu-id="50d19-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="50d19-108">Puede personalizar asignaciones de atributo predeterminadas Hola según las necesidades del negocio tooyour.</span><span class="sxs-lookup"><span data-stu-id="50d19-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="50d19-109">Esto significa que puede cambiar o eliminar asignaciones de atributos existentes o crear nuevas asignaciones de atributos.</span><span class="sxs-lookup"><span data-stu-id="50d19-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="50d19-110">En el portal de Azure AD hello, puede tener acceso a esta característica haciendo clic en un **asignaciones** configuración bajo **Provisioning** en hello **administrar** sección de un  **Aplicación empresarial**.</span><span class="sxs-lookup"><span data-stu-id="50d19-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="50d19-112">Al hacer clic en un **asignaciones** configuración, se abrirá Hola relacionados con **asignación de atributos** hoja.</span><span class="sxs-lookup"><span data-stu-id="50d19-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="50d19-113">No hay asignaciones de atributos que son requeridas por un toofunction de aplicación de SaaS correctamente.</span><span class="sxs-lookup"><span data-stu-id="50d19-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="50d19-114">Para los atributos necesarios, Hola **eliminar** característica no está disponible.</span><span class="sxs-lookup"><span data-stu-id="50d19-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="50d19-116">En el ejemplo de Hola anterior, puede ver que hello **nombre de usuario** atributo de un objeto administrado en Salesforce se rellena con hello **userPrincipalName** valor de hello vincula el objeto de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="50d19-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="50d19-117">Puede personalizar las **asignaciones de atributos** existentes haciendo clic en una asignación.</span><span class="sxs-lookup"><span data-stu-id="50d19-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="50d19-118">Se abrirá hello **Editar atributo** hoja.</span><span class="sxs-lookup"><span data-stu-id="50d19-118">This opens hello **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="50d19-120">Información sobre los tipos de asignación de atributos</span><span class="sxs-lookup"><span data-stu-id="50d19-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="50d19-121">Con asignaciones de atributos, puede controlar cómo se rellenan los atributos en una aplicación SaaS de terceros.</span><span class="sxs-lookup"><span data-stu-id="50d19-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="50d19-122">Se admiten cuatro tipos de asignaciones diferentes:</span><span class="sxs-lookup"><span data-stu-id="50d19-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="50d19-123">**Direct** : atributo de destino de Hola se rellena con el valor de Hola de un atributo del objeto vinculado Hola en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50d19-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="50d19-124">**Constante** : atributo de destino de Hola se rellena con una cadena específica que se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="50d19-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="50d19-125">**Expresión** -atributo de destino de Hola se rellena según el resultado de hello de una expresión de tipo de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="50d19-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="50d19-126">Para más información, consulte [Escritura de expresiones para la asignación de atributos en Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="50d19-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="50d19-127">**Ninguno** -Hola atributo de destino se deja sin modificar.</span><span class="sxs-lookup"><span data-stu-id="50d19-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="50d19-128">Sin embargo, si el atributo de destino de hello está vacío, se rellena con el valor predeterminado de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="50d19-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="50d19-129">En los tipos de asignación de suma toothese cuatro atributos básicos, asignaciones de atributo personalizadas admiten concepto de Hola de opcional **predeterminado** valor de asignación.</span><span class="sxs-lookup"><span data-stu-id="50d19-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="50d19-130">asignación de valor predeterminado de Hello garantiza que un atributo de destino se rellena con un valor si no hay ningún valor en Azure AD ni en el objeto de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="50d19-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="50d19-131">configuración más común de Hello es tooleave este en blanco.</span><span class="sxs-lookup"><span data-stu-id="50d19-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="50d19-132">Información sobre las propiedades de asignación de atributos</span><span class="sxs-lookup"><span data-stu-id="50d19-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="50d19-133">En la sección anterior de hello, ya han sido propiedad de tipo de asignación de atributo toohello se ha introducido.</span><span class="sxs-lookup"><span data-stu-id="50d19-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="50d19-134">En la propiedad toothis de adición, asignaciones de atributos también admiten Hola siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="50d19-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="50d19-135">**Atributo de origen** -atributo de usuario de Hola Hola sistema de origen (p. ej.: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="50d19-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="50d19-136">**Atributo de destino** : atributo de usuario de hello en el sistema de destino de hello (p. ej.: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="50d19-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="50d19-137">**Coincide con los objetos mediante este atributo** : si no se debe usar esta asignación toouniquely identificar a los usuarios entre los sistemas de origen y destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="50d19-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="50d19-138">Normalmente se establece en hello userPrincipalName o atributo de correo en Azure AD, que suele ser asignada tooa campo de nombre de usuario en una aplicación de destino.</span><span class="sxs-lookup"><span data-stu-id="50d19-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="50d19-139">**Precedencia de coincidencia**: se pueden establecer varios atributos coincidentes.</span><span class="sxs-lookup"><span data-stu-id="50d19-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="50d19-140">Si hay varios, se evalúan en orden de hello definido por este campo.</span><span class="sxs-lookup"><span data-stu-id="50d19-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="50d19-141">En el momento en que se encuentre una coincidencia, no se evaluarán más atributos coincidentes.</span><span class="sxs-lookup"><span data-stu-id="50d19-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="50d19-142">**Aplicar esta asignación**</span><span class="sxs-lookup"><span data-stu-id="50d19-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="50d19-143">**Siempre**: esta asignación se aplica a las acciones de creación y actualización de usuarios</span><span class="sxs-lookup"><span data-stu-id="50d19-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="50d19-144">**Solo durante la creación**: esta asignación se aplica solo a las acciones de creación de usuarios</span><span class="sxs-lookup"><span data-stu-id="50d19-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="50d19-145">Qué debería saber</span><span class="sxs-lookup"><span data-stu-id="50d19-145">What you should know</span></span>

<span data-ttu-id="50d19-146">Microsoft Azure AD proporciona una implementación eficaz de un proceso de sincronización.</span><span class="sxs-lookup"><span data-stu-id="50d19-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="50d19-147">En un entorno inicializado, sólo los objetos que requieren actualizaciones se procesan durante un ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="50d19-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="50d19-148">Actualizar asignaciones de atributos tiene un impacto en el rendimiento de Hola de un ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="50d19-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="50d19-149">Una configuración de asignación de actualización toohello atributo requiere vuelven a evaluar todas las toobe de objetos administrados.</span><span class="sxs-lookup"><span data-stu-id="50d19-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="50d19-150">Es un mejor práctica tookeep Hola número recomendado de asignaciones de atributos de cambios consecutivos tooyour como mínimo.</span><span class="sxs-lookup"><span data-stu-id="50d19-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50d19-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50d19-151">Next steps</span></span>

* [<span data-ttu-id="50d19-152">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50d19-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="50d19-153">Automatizar aplicaciones del usuario aprovisionamiento o desaprovisionamiento tooSaaS</span><span class="sxs-lookup"><span data-stu-id="50d19-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="50d19-154">Escritura de expresiones para la asignación de atributos</span><span class="sxs-lookup"><span data-stu-id="50d19-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="50d19-155">Filtros de ámbito para el aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="50d19-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="50d19-156">Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="50d19-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="50d19-157">Notificaciones de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="50d19-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="50d19-158">Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="50d19-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

