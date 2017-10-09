# Información general
## [Herramientas de supervisión en Azure](monitoring-overview.md)
## [Azure Monitor](monitoring-overview-azure-monitor.md)
## [Métricas](monitoring-overview-metrics.md)
## [Alertas](monitoring-overview-alerts.md)
## [Autoscale](monitoring-overview-autoscale.md)
## [Registro de actividad](monitoring-overview-activity-logs.md)
## [Grupos de acciones](monitoring-action-groups.md)
## [Registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md)
## [Integraciones de asociados](monitoring-partners.md)
## [Extensión de Diagnósticos de Azure](azure-diagnostics.md)


# Introducción
## [Introducción a Azure Monitor](monitoring-get-started.md)
## [Introducción al escalado automático](monitoring-autoscale-get-started.md)
## [Permisos de roles y seguridad](monitoring-roles-permissions-security.md)


# Procedimientos
## Usar alertas
### [Configuración de alertas en Azure Portal](insights-alerts-portal.md)
### [Configuración de alertas con CLI](insights-alerts-command-line-interface.md)
### [Configuración de alertas con PowerShell](insights-alerts-powershell.md)
### [Llamada de una alerta métrica a un webhook](insights-webhooks-alerts.md)
### [Creación de una alerta de métrica con una plantilla de Resource Manager](monitoring-enable-alerts-using-template.md)
## Usar Autoscale
### [Procedimientos recomendados](insights-autoscale-best-practices.md)
### [Métricas comunes](insights-autoscale-common-metrics.md)
### [Patrones comunes](monitoring-autoscale-common-scale-patterns.md)
### [Escalado automático con una métrica personalizada](monitoring-autoscale-scale-by-custom-metric.md)
### [Escalado automático de conjuntos de escalado de máquinas virtuales con plantillas de Resource Manager](insights-advanced-autoscale-virtual-machine-scale-sets.md)
### [Escalado automático de máquinas en un conjunto de escalado de máquinas virtuales](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json)
### [Configuración de webhooks y notificaciones por correo electrónico en escalado automático](insights-autoscale-to-webhook-email.md)
## Usar el registro de actividad de Hola
### [Visualización de eventos en el registro de actividad](../azure-resource-manager/resource-group-audit.md?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json)
### [Configuración de alertas en un evento del registro de actividad](monitoring-activity-log-alerts.md)
### [Archivo del registro de actividad](monitoring-archive-activity-log.md)
### [TooEvent de registro de actividad de flujo centros](monitoring-stream-activity-logs-event-hubs.md)
### [Operaciones de auditoría con Resource Manager](../azure-resource-manager/resource-group-audit.md?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json)
### [Creación de alertas del registro de actividad con Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
### [Migrar las alertas de registro de tooActivity](monitoring-migrate-management-alerts.md)
## Uso de notificaciones de servicio
### [Visualización de notificaciones de servicio](monitoring-service-notifications.md)
### [Configuración de alertas en notificaciones de servicio](monitoring-activity-log-alerts-on-service-notifications.md)
## Uso de grupos de acciones
### [Información acerca del esquema de webhook](monitoring-activity-log-alerts-webhook.md)
### [Comportamiento de alertas por SMS](monitoring-sms-alert-behavior.md)
### [Limitación de índice de alertas](monitoring-alerts-rate-limiting.md)
### [Creación de grupos de acciones con Resource Manager](monitoring-create-action-group-with-resource-manager-template.md)
## Administración de registros de diagnósticos
### [Archivar](monitoring-archive-diagnostic-logs.md)
### [Secuencia tooEvent centros](monitoring-stream-diagnostic-logs-to-event-hubs.md)
### [Habilitación de la configuración de diagnóstico mediante plantillas de Resource Manager](monitoring-enable-diagnostic-logs-using-template.md)
## Usar hello API de REST
### [Tutorial con la API de REST](monitoring-rest-api-walkthrough.md)
## Uso de la extensión de Diagnósticos de Azure
### [Enviar información de tooApplication](azure-diagnostics-configure-application-insights.md)
### [Enviar tooEvent centros](azure-diagnostics-streaming-event-hubs.md)
### [Solución de problemas](azure-diagnostics-troubleshooting.md)

# Referencia
## [Ejemplos de código](https://azure.microsoft.com/en-us/resources/samples/?service=monitor)
## [Orígenes de datos de supervisión](monitoring-data-sources.md)
## [Lista de métricas compatibles](monitoring-supported-metrics.md)
## [Esquema de evento del registro de actividad](monitoring-activity-log-schema.md)
## [Servicios admitidos, categorías y esquemas para los registros de diagnóstico](monitoring-diagnostic-logs-schema.md)
## [PowerShell](/powershell/module/azurerm.insights)
## [.NET](https://msdn.microsoft.com/library/azure/dn802153)
## [REST](/rest/api/monitor/)
## [Esquema de extensión de Azure Diagnostics](azure-diagnostics-schema.md)
### [1.0](azure-diagnostics-schema-1dot0.md)
### [1.2](azure-diagnostics-schema-1dot2.md)
### [1.3 y versiones posteriores](azure-diagnostics-schema-1dot3-and-later.md)

# Recursos
## [Ejemplos de la CLI de Azure 1.0](insights-cli-samples.md)
## [Azure Roadmap](https://azure.microsoft.com/roadmap/?category=monitoring-management)
## [Ejemplos de PowerShell](insights-powershell-samples.md)
## [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/)
## [Vídeos](https://azure.microsoft.com/resources/videos/index/?services=monitor)
## [Plantillas de inicio rápido](https://azure.microsoft.com/en-us/resources/templates/?resourceType=Microsoft.Insights)
