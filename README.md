# Investigación: Análisis de GNS3 e Hipervisores (Windows 11)

Este repositorio contiene la **investigación técnica** sobre la integración de GNS3 con distintos entornos de virtualización, analizando su arquitectura y optimización en sistemas Windows 11 para la carrera de **Ingeniería de Ciberseguridad**.

---

### 1. Fundamentos de Virtualización en Windows 11
La investigación determinó que para un entorno de emulación profesional, la base reside en la correcta interacción entre el hardware y el software:
* **Capa de Hardware:** La habilitación de VT-x/AMD-V en la BIOS es el requisito primario.
* **Seguridad del SO:** Se analizó el impacto del "Aislamiento de núcleo", el cual debe ser compatible con las extensiones de virtualización para evitar conflictos de rendimiento.

### 2. Análisis del Motor: GNS3 VM y Soporte KVM
Se investigó la importancia de la **GNS3 VM** como el componente que gestiona los nodos de red de manera nativa. 

Un punto crítico de la investigación fue la validación del **Soporte KVM**. Como se observa en la captura técnica adjunta, el estado `True` confirma que el hipervisor permite la aceleración por hardware, permitiendo que las máquinas virtuales de red funcionen con la velocidad del procesador físico:
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/8a805c17-06e5-4f01-9af1-a96a48252c37" />

---

### 3. Comparativa de Hipervisores Investigados
* **VirtualBox (Tipo 2):** Se analizó su flexibilidad en entornos de desarrollo. Se destaca la necesidad técnica del **Modo Promiscuo** para permitir el paso de tráfico de Capa 2 (tramas Ethernet) entre routers virtuales.
* **VMware ESXi (Tipo 1):** Investigado como la solución de alto rendimiento. Al ser un hipervisor "Bare Metal", ofrece una gestión más eficiente de los recursos mediante la API en el puerto **3080**.
<img width="1004" height="781" alt="image" src="https://github.com/user-attachments/assets/c33d5db4-27fb-42fd-b595-1e80283ccb64" />

### 4. Matriz de Soluciones Técnicas (Troubleshooting)

| Hallazgo | Causa Técnica | Resolución Propuesta |
| :--- | :--- | :--- |
| **KVM disponible: False** | Incompatibilidad de virtualización anidada. | Habilitar `nested-hw-virt` mediante CLI. |
| **Fallo de conexión API** | Restricciones de red en el puerto 3080. | Apertura de puertos en el Firewall local. |
| **Aislamiento de Tráfico** | Desactivación de modo promiscuo. | Ajuste del adaptador a "Permitir todo". |

 ### Diagrama de Arquitectura del Sistema

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/e5b68001-3e57-4f49-b9a3-3478998abca6" />

###  Descripción del Diagrama

El diagrama muestra la estructura del sistema implementado. El usuario interactúa con GNS3 desde Windows 11, el cual utiliza un hipervisor de tipo 2 (VirtualBox o VMware) para ejecutar la GNS3 VM.

Dentro de la GNS3 VM se ejecutan los dispositivos de red utilizando KVM para mejorar el rendimiento. De manera opcional, se puede integrar un servidor ESXi (tipo 1) para manejar laboratorios más complejos.
