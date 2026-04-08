Investigación: GNS3 e Hipervisores (Windows 11)
Este documento detalla la configuración y optimización de un entorno de emulación de redes profesional, enfocado en la integración de GNS3 con distintos hipervisores.

1. Arquitectura de Virtualización en Windows 11
Para garantizar que los laboratorios de red funcionen con alto rendimiento, se deben cumplir los siguientes requisitos de hardware y software:

Virtualización en BIOS/UEFI: Debe estar habilitada (VT-x para Intel o AMD-V) para que el hipervisor acceda directamente al procesador.

Aislamiento de Núcleo: Se recomienda verificar que esta función de seguridad de Windows no bloquee los recursos necesarios para VirtualBox o VMware.

2. GNS3 VM: El Motor de Simulación
La GNS3 VM es el componente principal que ejecuta los nodos de red (Routers, Switches, Firewalls) de forma eficiente.

Soporte KVM: Es fundamental que el estado aparezca como True. Esto garantiza la aceleración por hardware nativa, permitiendo ejecutar imágenes QEMU/KVM con fluidez.

Recursos Asignados: Se recomienda un mínimo de 4GB de RAM y 2 vCPUs para laboratorios básicos.

3. Integración con Hipervisores
VirtualBox (Tipo 2)
Es la opción preferida para entornos de aprendizaje rápido.

Adaptador Host-Only: Permite la comunicación entre la laptop física y la VM.

Modo Promiscuo: Debe configurarse en "Permitir todo" para que el tráfico de Capa 2 sea procesado correctamente por los routers virtuales.

VMware ESXi (Tipo 1)
A diferencia de los hipervisores de escritorio, ESXi corre directamente sobre el hardware (Bare Metal).

Gestión: La conexión se realiza mediante la IP del servidor y el puerto 3080.

Rendimiento: Ideal para simulaciones complejas que requieren alta disponibilidad de recursos.
