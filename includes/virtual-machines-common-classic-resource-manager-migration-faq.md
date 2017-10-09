# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Preguntas más frecuentes sobre la migración del Administrador de recursos de tooAzure clásico

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>¿Afecta este plan de migración a alguno de los servicios o las aplicaciones existentes que se ejecutan en máquinas virtuales de Azure? 

No. las máquinas virtuales de Hello (clásicas) son servicios totalmente compatibles en disponibilidad general. Puede seguir estos recursos tooexpand toouse la superficie en Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>¿Qué ocurre toomy las máquinas virtuales si no va a migrar en hello futuro próximo? 

No nos estamos dejando Hola clásico recursos y las API de modelo existente. Queremos toomake migración fácil, teniendo en cuenta Hola características avanzadas que están disponibles en el modelo de implementación del Administrador de recursos de Hola. Es muy recomendable que revise [algunos de los avances de hello](../articles/azure-resource-manager/resource-manager-deployment-model.md) que forman parte de IaaS en el Administrador de recursos.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>¿Qué supone este plan de migración para las herramientas existentes? 

Actualización del modelo de implementación del Administrador de recursos de toohello de herramientas es uno de los cambios de más importantes de Hola que tienen tooaccount para en sus planes de migración.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>¿Cuánto tiempo será el tiempo de inactividad de hello plano de administración? 

Depende de número de Hola de recursos que se van a migrar. Para implementaciones más pequeñas (de unas decenas de máquinas virtuales), migración completa Hola tardará menos de una hora. Para implementaciones a gran escala (cientos de máquinas virtuales), migración de hello puede tardar unas horas.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>¿Puedo revertir el proceso después de que la migración de los recursos esté confirmada en Resource Manager? 

Puede anular la migración siempre que sean recursos Hola Hola preparado estado. No se admite la reversión después de recursos de Hola se han migrado correctamente a través de la operación de confirmación de Hola.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>¿Deshacer mi migración si se produce un error en la operación de confirmación de hello? 

No se puede anular la migración si se produce un error en la operación de confirmación de Hola. Todas las operaciones de migración, incluidas la operación de confirmación de hello, son idempotentes. Por lo tanto, se recomienda que vuelva a intentar la operación de hello después de unos minutos. Si todavía se enfrenta a un error, cree una incidencia de soporte técnico o crear una entrada de foro con hello ClassicIaaSMigration etiqueta en nuestro [foro de la máquina virtual](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>¿Tengo toobuy otro circuito de express route si tengo toouse en el Administrador de recursos de IaaS? 

No. Se ha habilitado recientemente [mover circuitos ExpressRoute de modelo de implementación de administrador de recursos de hello toohello clásico](../articles/expressroute/expressroute-move.md). No tiene un nuevo circuito de ExpressRoute de toobuy si ya tiene una.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>¿Qué ocurre si había configurado las directivas de control de acceso basado en rol para mis recursos IaaS clásicos? 

Durante la migración, los recursos de Hola transforman de clásico tooResource Manager. Por lo tanto, se recomienda que planee las actualizaciones de directiva RBAC Hola que necesitan toohappen después de la migración.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>He realizado copias de seguridad de mis máquinas virtuales clásicas en un almacén de Backup. ¿Puedo migrar Mis máquinas virtuales de modo de administrador de tooResource de modo clásico y protegerlos en un almacén de servicios de recuperación? 

Clásicos puntos de recuperación de máquina virtual en un almacén de copia de seguridad no migran automáticamente tooa el almacén de servicios de recuperación cuando se mueve Hola VM de clásico tooResource modo de administrador. Siga estos pasos tootransfer las copias de seguridad de máquina virtual:

1. En el almacén de copia de seguridad de hello, vaya toohello **elementos protegidos** pestaña y seleccione Hola máquina virtual. Haga clic en [Detener protección](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deje la opción *Eliminar los datos de copia de seguridad asociados***desactivada**.
2. Eliminar la extensión de copia de seguridad o instantánea de Hola de hello máquina virtual.
3. Migrar máquina virtual de Hola de modo de administrador de tooResource de modo clásico. Asegúrese de migrar la información de red y almacenamiento de hello, máquina virtual de toohello correspondiente también es tooResource el modo de administrador.
4. Crear un almacén de servicios de recuperación y configurar copia de seguridad en hello migrar máquina virtual usando **copia de seguridad** acción sobre el panel almacén. Para obtener información detallada sobre la copia de seguridad de los servicios de recuperación de tooa de una máquina virtual del almacén, consulte el artículo de hello, [proteger máquinas virtuales de Azure con un almacén de servicios de recuperación](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>¿Validar mi suscripción o recursos toosee si son capaces de migración? 

Sí. En la opción de migración admitida por la plataforma de hello, Hola primer paso en la preparación para la migración es toovalidate que los recursos de hello son capaces de migración. En caso de hello validar la operación se produce un error, recibir mensajes para todos los motivos de hello no se puede completar la migración de Hola.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>¿Qué ocurre si experimenta un error de cuota al preparar los recursos de IaaS de hello para la migración? 

Se recomienda que anule la migración y, a continuación, inicie sesión un cuotas de soporte técnico solicitud tooincrease Hola Hola región Hola migrar máquinas virtuales. Después de que se apruebe la solicitud de cuota de hello, puede empezar a ejecutar pasos de migración de hello nuevo.

## <a name="how-do-i-report-an-issue"></a>¿Cómo se informa de un problema? 

Registrar los problemas y preguntas sobre migración tooour [foro VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), con la palabra clave de hello ClassicIaaSMigration. Se recomienda registrar todas sus preguntas en este foro. Si tiene un contrato de soporte técnico, dispone de bienvenida toolog así una incidencia de soporte técnico.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>¿Qué ocurre si no me gusta nombres Hola de recursos de Hola Hola plataforma elegido durante la migración? 

Todos los recursos de hello proporcionar explícitamente los nombres en el modelo de implementación clásica de Hola se conservan durante la migración. En algunos casos, se crean recursos nuevos. Por ejemplo, se crea una interfaz de red para cada máquina virtual. Actualmente no admitimos hello capacidad toocontrol Hola los nombres de estos recursos nuevos creados durante la migración. Registrar los votos para esta característica de hello [foro de comentarios Azure](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>¿Puedo migrar circuitos de ExpressRoute utilizados en las suscripciones con vínculos de autorización? 

Los circuitos de ExpressRoute que usan vínculos de autorización entre suscripciones no se pueden migrar automáticamente sin tiempo de inactividad. Contamos con instrucciones sobre cómo se pueden migrar mediante pasos manuales. Vea [ExpressRoute migrar circuitos y asociado redes virtuales de modelo de implementación de administrador de recursos de hello toohello clásico](../articles/expressroute/expressroute-migration-classic-resource-manager.md) pasos y más información.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Recibí un mensaje *"VM está informando de hello general como el estado del agente no está listo. Por lo tanto, no se pueden migrar Hola máquina virtual. Asegúrese de que ese agente de máquina virtual de hello es informar del estado de agente global como listo"* o *"máquina virtual contiene extensión cuyo estado no se está informando de hello máquina virtual. Por lo tanto, esta máquina virtual no se puede migrar." *

Este mensaje se recibe cuando Hola VM no tiene conectividad saliente toohello internet. agente de máquina virtual de Hello usa la cuenta de almacenamiento de Azure de conectividad saliente tooreach Hola para actualizar el estado del agente de hello cada cinco minutos.
