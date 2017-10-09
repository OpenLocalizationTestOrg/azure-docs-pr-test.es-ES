Hola según los requisitos de Hola de listas de tabla para puertas de enlace PolicyBased y RouteBased VPN. Esta tabla aplica tooboth Hola Administrador de recursos y modelos de implementación clásica. Para el modelo clásico de hello, puertas de enlace PolicyBased VPN se Hola igual como puertas de enlace estáticas y puertas de enlace de ruta se Hola igual como puertas de enlace dinámicos.

|  | **Puerta de enlace de VPN básica basada en directivas** | **Puerta de enlace de VPN básica basada en enrutamientos** | **Puerta de enlace de VPN estándar basada en enrutamientos** | **Puerta de enlace de VPN de alto rendimiento basada en enrutamientos** |
| --- | --- | --- | --- | --- |
| **Conectividad de sitio a sitio...(S2S)** |Configuración de VPN de PolicyBased |Configuración de VPN de RouteBased |Configuración de VPN de RouteBased |Configuración de VPN de RouteBased |
| **Conectividad de punto a sitio (P2S**) |No compatible |Compatible (puede coexistir con S2S) |Compatible (puede coexistir con S2S) |Compatible (puede coexistir con S2S) |
| **Método de autenticación** |Clave precompartida |Clave precompartida para la conectividad de S2S, Certificados para la conectividad de P2S |Clave precompartida para la conectividad de S2S, Certificados para la conectividad de P2S |Clave precompartida para la conectividad de S2S, Certificados para la conectividad de P2S |
| **Número máximo de conexiones S2S** |1 |10 |10 |30 |
| **Número máximo de conexiones P2S** |No compatible |128 |128 |128 |
| **Compatibilidad con enrutamiento activo (BGP)** |No compatible |No compatible |Compatible |Compatible |

