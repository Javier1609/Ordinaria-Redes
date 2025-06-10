# Solución del Examen de Redes

## Parte IV: Cálculo del Tamaño de Ventana y Congestión

### **Pregunta 15. Cálculo del Tamaño de Ventana y Congestión**

#### a) Conversión de unidades:
- **RTT**: 50 ms = \(50 \times 10^{-3}\) segundos = 0.05 segundos.
- **Ancho de banda**: 100 Mbps = \(100 \times 10^6\) bits por segundo.
- **MSS**: 1,500 bytes = \(1,500 \times 8 = 12,000\) bits.

#### b) Tamaño óptimo de la ventana:
\[
\text{Ventana óptima} = \text{Ancho de banda} \times \text{RTT}
\]
Sustituyendo los valores:
\[
\text{Ventana óptima} = 100 \times 10^6 \times 0.05 = 5 \times 10^6 \, \text{bits}
\]
En bytes:
\[
\text{Ventana óptima} = \frac{5 \times 10^6}{8} = 625,000 \, \text{bytes}
\]

#### c) Número de segmentos MSS en tránsito:
\[
\text{Segmentos en tránsito} = \frac{\text{Ventana óptima en bytes}}{\text{MSS}}
\]
Sustituyendo los valores:
\[
\text{Segmentos en tránsito} = \frac{625,000}{1,500} \approx 416.67 \, \text{segmentos}
\]
Aproximadamente **416 segmentos MSS** pueden estar en tránsito simultáneamente.

#### d) Relación con el control de congestión:
El tamaño de ventana óptimo es crucial para evitar congestión en TCP. Si la ventana es demasiado grande, puede saturar la red, mientras que una ventana pequeña limita el rendimiento. TCP ajusta dinámicamente la ventana para equilibrar la eficiencia y evitar congestión.

---

### **Pregunta 16. Mecanismos de Control de Congestión en TCP**

#### **Algoritmo de Arranque Lento (Slow Start)**:
- **Objetivo**: Evitar saturar la red al inicio de la conexión.
- **Funcionamiento**: La ventana de congestión comienza con un tamaño pequeño y se incrementa exponencialmente hasta alcanzar el umbral de congestión.

#### **Algoritmo de Nagle**:
- **Objetivo**: Reducir el número de pequeños paquetes enviados.
- **Funcionamiento**: Agrupa pequeños paquetes en uno más grande antes de enviarlo, optimizando el uso del ancho de banda.

#### **Algoritmo de Clark**:
- **Objetivo**: Evitar el envío de paquetes pequeños cuando hay datos pendientes.
- **Funcionamiento**: Retrasa el envío de paquetes pequeños hasta que se acumule suficiente información.

---

## Parte V: Capa de Aplicación y Aplicaciones Multimedia

### **Pregunta 17. Protocolos de Correo y Funcionamiento de HTTP/FTP**

#### a) Comparación de POP3, IMAP y SMTP:
| **Protocolo** | **Función** | **Modo de operación** | **Ejemplo de uso** |
|---------------|-------------|-----------------------|--------------------|
| **POP3**      | Recuperar correos. | Descarga y elimina correos del servidor. | Cliente de correo local. |
| **IMAP**      | Recuperar correos. | Sincroniza correos entre servidor y cliente. | Acceso desde múltiples dispositivos. |
| **SMTP**      | Enviar correos.    | Transfiere correos entre servidores. | Envío de correos electrónicos. |

#### b) Funcionamiento de HTTP y FTP:
- **HTTP**:
  - Utiliza métodos como `GET`, `POST`, `PUT`, `DELETE` para interactuar con recursos web.
  - Usa una única conexión para enviar solicitudes y recibir respuestas.

- **FTP**:
  - Usa dos conexiones: una para control y otra para transferencia de datos.
  - Permite transferir archivos entre cliente y servidor.

---

### **Pregunta 18. Streaming y VoIP**

#### a) Tipos de streaming:
| **Tipo**               | **Definición** | **Ejemplo** |
|------------------------|----------------|-------------|
| **UDP Streaming**      | Transmisión rápida sin garantía de entrega. | Streaming en tiempo real. |
| **HTTP Streaming**     | Usa HTTP para transferir contenido multimedia. | YouTube. |
| **Adaptive HTTP Streaming (DASH)** | Ajusta la calidad según el ancho de banda disponible. | Netflix. |

#### b) Funcionamiento de VoIP:
- **Proceso**: Convierte la voz en paquetes de datos, los transmite por la red y los reconstruye en el receptor.
- **Problemas comunes**:
  - **Retardo**: Solución: Usar redes de baja latencia.
  - **Pérdida de paquetes**: Solución: Implementar retransmisión o corrección de errores.

---

### **Pregunta 19. Control de Congestión en Redes Multimedia y Modelos de Calidad de Servicio**

#### a) Técnicas para evitar congestión:
1. **Buffering en el cliente**: Almacena datos antes de reproducirlos para evitar interrupciones.
2. **Marcado de paquetes mediante DiffServ**: Prioriza paquetes según su importancia.

#### b) Comparación de modelos:
| **Modelo**       | **Tráfico** | **Garantía de calidad** | **Ejemplo** |
|------------------|-------------|-------------------------|-------------|
| **Best-Effort**  | No prioriza tráfico. | Sin garantía. | Navegación web. |
| **Servicios Multiclase** | Prioriza tráfico según clases. | Garantía parcial. | Streaming multimedia. |

---

## Parte VI: Seguridad en Redes

### **Pregunta 20. Problemas Críticos de Seguridad y Soluciones**

| **Área**          | **Descripción** | **Solución** |
|-------------------|-----------------|--------------|
| **Confidencialidad** | Proteger datos de accesos no autorizados. | Cifrado (AES). |
| **Autenticación**   | Verificar identidad. | Certificados digitales. |
| **No repudio**      | Garantizar que el remitente no pueda negar el envío. | Firmas digitales. |
| **Integridad**      | Asegurar que los datos no sean modificados. | Hashing (SHA-256). |

---

### **Pregunta 21. Cifrado Simétrico vs. Asimétrico**

| **Aspecto**         | **Simétrico** | **Asimétrico** |
|---------------------|---------------|----------------|
| **Número de claves** | 1 clave.      | 2 claves (pública y privada). |
| **Velocidad**        | Más rápido.   | Más lento. |
| **Ejemplos**         | AES, DES.     | RSA, ECC. |
| **Aplicaciones**     | Cifrado de datos. | Firmas digitales. |

---

### **Pregunta 22. Funcionamiento del Algoritmo RSA**

#### a) Proceso de generación de claves:
1. Seleccionar dos números primos (\(p\) y \(q\)).
2. Calcular \(n = p \times q\).
3. Calcular \(\phi(n) = (p-1) \times (q-1)\).
4. Elegir \(e\) tal que \(1 < e < \phi(n)\) y \(e\) sea coprimo con \(\phi(n)\).
5. Calcular \(d\) tal que \(d \times e \mod \phi(n) = 1\).

#### b) Ejemplo numérico:
- \(p = 3\), \(q = 11\), \(e = 7\), \(M = 4\).
- \(n = 3 \times 11 = 33\).
- \(\phi(n) = (3-1) \times (11-1) = 20\).
- \(d = 3\) (porque \(7 \times 3 \mod 20 = 1\)).
- **Cifrado**: \(C = M^e \mod n = 4^7 \mod 33 = 16\).
- **Descifrado**: \(M = C^d \mod n = 16^3 \mod 33 = 4\).

---

### **Pregunta 23. Firewalls, VPN, IPSec y SSL/TLS**

#### a) Firewalls:
- **Filtrado de paquetes**: Inspecciona cada paquete según reglas predefinidas.
- **Firewall de estado**: Monitorea el estado de las conexiones activas.

#### b) VPN vs. IPSec:
| **Aspecto** | **VPN** | **IPSec** |
|-------------|---------|-----------|
| **Propósito** | Crear redes privadas. | Proteger datos en redes públicas. |
| **Modo de operación** | Túneles cifrados. | Cifrado de paquetes. |

#### c) SSL/TLS:
- **Funcionamiento**: Establece un canal cifrado entre cliente y servidor.
- **Importancia**: Protege datos sensibles en comunicaciones web.

---

### **Pregunta 24. DNS Spoofing y Protección con DNSSEC**

#### a) DNS Spoofing:
- **Descripción**: Ataque que redirige a usuarios a sitios falsos mediante respuestas DNS manipuladas.
- **Impacto**: Compromete la integridad de las comunicaciones.

#### b) DNSSEC:
- **Descripción**: Usa firmas digitales para verificar la autenticidad de las respuestas DNS.
- **Beneficio**: Previene ataques de suplantación.
