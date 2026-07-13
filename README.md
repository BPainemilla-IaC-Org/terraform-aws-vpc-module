# 🌐 AWS Networking Module (VPC)

Este módulo reutilizable de Terraform automatiza el aprovisionamiento de una topología de red estándar y segura en Amazon Web Services (AWS), aislando las cargas de trabajo según las mejores prácticas de la industria.

## 🗺️ Diagrama de Arquitectura de Red

El módulo genera una infraestructura de red segmentada de la siguiente manera:

```text
[Internet]
    │
[Internet Gateway (IGW)]
    │
┌───▼────────────────────────────────────────────────────────┐
│ VPC (Virtual Private Cloud)                                │
│                                                            │
│ ┌─────────────────────────┐   ┌──────────────────────────┐ │
│ │ Subnet Pública A (AZ1)  │   │ Subnet Pública B (AZ2)   │ │
│ │                         │   │                          │ │
│ │  [Tabla de Ruteo Main]  │   │  [Tabla de Ruteo Main]   │ │
│ └─────────────────────────┘   └──────────────────────────┘ │
└────────────────────────────────────────────────────────────┘

🚀 Parámetros y Componentes Desplegados

Virtual Private Cloud (VPC): Segmento de red lógica aislado con direccionamiento CIDR parametrizable.

Subredes Públicas: Dos subredes distribuidas en diferentes Zonas de Disponibilidad (AZ) para garantizar alta disponibilidad.

Internet Gateway (IGW): Permite la comunicación bidireccional entre los recursos dentro de la VPC y la red pública de Internet.

Tablas de Enrutamiento: Tablas con rutas explícitas que asocian las subredes públicas directamente hacia el IGW.

🛠️ Variables de Entrada (Inputs)
┌───────────────────────────────────────────────────────────────────────────────────────────────────────┐
|  Nombre           |          Descripción                 |       Tipo          |       Defecto        |
|───────────────────────────────────────────────────────────────────────────────────────────────────────|
|  vpc_cidr_block   | Bloque CIDR base de la VPC           |      string        |         N/A           |
|───────────────────────────────────────────────────────────────────────────────────────────────────────|
|  vpc_name         | Etiqueta identificadora para la VPC  |      string        |         N/A           |
|───────────────────────────────────────────────────────────────────────────────────────────────────────|
|  subnet_a_cidr    | Bloque CIDR para la Subred Pública A |      string        |         N/A           |
|───────────────────────────────────────────────────────────────────────────────────────────────────────|
|  subnet_b_cidr    | Bloque CIDR para la Subred Pública B |      string        |         N/A           |
└───────────────────────────────────────────────────────────────────────────────────────────────────────┘

📤 Variables de Salida (Outputs)
┌────────────────────────────────────────────────────────────────────────────────────────┐
|  Nombre              |                 Descripción                                     |
|────────────────────────────────────────────────────────────────────────────────────────|
|  vpc_id              | Identificador único de la VPC creada en AWS.                    |
|────────────────────────────────────────────────────────────────────────────────────────|
|  subnet_public_a_id  | ID de la subred pública ubicada en la Zona de Disponibilidad A. |
|────────────────────────────────────────────────────────────────────────────────────────|
|  subnet_public_b_id  | ID de la subred pública ubicada en la Zona de Disponibilidad B. |
└────────────────────────────────────────────────────────────────────────────────────────┘
