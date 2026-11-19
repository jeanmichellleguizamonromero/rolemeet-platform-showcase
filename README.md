# 🏛️ RoLEMeet — Plataforma WebRTC para Asambleas de Propiedad Horizontal

[![Node.js](https://img.shields.io/badge/Node.js-v18+-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express.js-Backend-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![Firebase](https://img.shields.io/badge/Firebase-Admin_SDK-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/)
[![LiveKit](https://img.shields.io/badge/LiveKit-WebRTC_Media-00E599)](https://livekit.io/)
[![Security](https://img.shields.io/badge/Security-JWT_%7C_Bcrypt_%7C_Forge-red)](https://github.com/)

> **RoLEMeet** es un ecosistema SaaS diseñado para transformar la toma de decisiones en copropiedades y entidades corporativas, eliminando el fraude en quórum, agilizando votaciones complejas y ofreciendo transmisión de audio/video en tiempo real con ultra baja latencia.

🔗 **Plataforma en Producción:** [rolesaas.com/meet](https://rolesaas.com/meet/)  
💼 **Desarrollado por:** LR Reuniones y Asambleas / BYO Improvement  

---

## 📌 El Problema de Negocio

Las asambleas de propiedad horizontal enfrentan desafíos operacionales y jurídicos críticos:
1. **Falta de Validez Jurídica:** Votaciones manuales o por chat que carecen de trazabilidad y generan impugnaciones legales (Ley 675 de 2001).
2. **Cálculo Complejo de Quórum:** Computar coeficientes de copropiedad al milisegundo ante la llegada de nuevos asistentes o cesión de poderes.
3. **Fricción Tecnológica:** Plataformas tradicionales (Zoom/Teams) no están diseñadas para votaciones ponderadas por coeficiente ni control estricto de oradores.

---

## 🚀 Arquitectura y Capacidades Técnicas

```mermaid
flowchart TD
    subgraph Clientes ["📱 Frontend (React & Lucide UI)"]
        Admin["Panel Administrador / Mesa Directiva"]
        User["Portal Copropietario / Votante"]
    end

    subgraph BackendGateway ["⚙️ Backend API Gateway (Node.js & Express)"]
        Auth["Seguridad & Auth\n(JWT + Bcrypt + Node-Forge)"]
        Quorum["Motor de Quórum & Coeficientes\n(Cálculo en Tiempo Real)"]
        Voting["Módulo de Votación Ponderada"]
        DocHandler["Gestión de Poderes y Actas\n(Multer & Mime-Types)"]
    end

    subgraph CloudMedia ["☁️ Servicios Cloud & Streaming"]
        Firebase[("Firebase Firestore & Realtime DB")]
        LiveKit["Servidor SFU WebRTC (LiveKit)\n(Audio/Video Ultra Baja Latencia)"]
        GoogleAPIs["Google APIs & Cloud Services"]
    end

    User <-->|HTTP / WebSockets| Auth
    Admin <-->|Gestión de Asamblea| Quorum
    Auth --> Voting
    DocHandler --> Firebase
    Voting --> Firebase
    User <-->|Transmisión WebRTC| LiveKit
    Admin <-->|Moderación y Transmisión| LiveKit
    BackendGateway <--> GoogleAPIs
```

## 📸 Vitrina Visual de la Plataforma

### 🗳️ Votación Ponderada en Tiempo Real
![Votación en vivo](docs/07_%20Livevoting.png)

### 🖥️ Módulos de Operación, Control y Experiencia de Usuario

<table>
  <tr>
    <td width="50%" align="center">
      <strong>1. Agenda del Conductor</strong><br><br>
      <img src="docs/01_%20Agenda%20Conductor.png" alt="Agenda del Conductor" width="100%" /><br>
      <sub>Gestión de orden del día y tiempos</sub>
    </td>
    <td width="50%" align="center">
      <strong>2. Dashboard de Operaciones</strong><br><br>
      <img src="docs/02_%20Operationsdashboard.png" alt="Dashboard de Operaciones" width="100%" /><br>
      <sub>Monitoreo operativo de la asamblea</sub>
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <strong>3. Expediente Digital</strong><br><br>
      <img src="docs/03_%20Expedientedigital.png" alt="Expediente Digital" width="100%" /><br>
      <sub>Trazabilidad documental y actas</sub>
    </td>
    <td width="50%" align="center">
      <strong>4. Portal del Participante (Móvil / Web)</strong><br><br>
      <img src="docs/04_%20Participant-app.png" alt="Portal del Participante" width="100%" /><br>
      <sub>Interfaz accesible para copropietarios</sub>
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <strong>5. Equipo, Roles y Permisos</strong><br><br>
      <img src="docs/05_%20Equipo%20y%20Roles.png" alt="Equipo y Roles" width="100%" /><br>
      <sub>Control de mesa directiva y moderadores</sub>
    </td>
    <td width="50%" align="center">
      <strong>6. Votación y Transcripción en Vivo</strong><br><br>
      <img src="docs/06_%20AgendaconductorVotacionytranscripcionenvivo.png" alt="Votación y Transcripción" width="100%" /><br>
      <sub>Registro automatizado de intervenciones</sub>
    </td>
  </tr>
</table>

🛡️ Módulos de Ingeniería Destacados

1. Seguridad Criptográfica y Validez Legal
Autenticación sin Estado (Stateless Auth): Implementación de tokens firmados mediante jsonwebtoken (JWT) con hashing de credenciales en bcrypt.
Integridad Criptográfica: Uso de node-forge para la verificación criptográfica y firma digital de actas y resultados de votación, blindando las decisiones contra repudiación jurídica.
2. Infraestructura de Medios en Tiempo Real (LiveKit / WebRTC)
Despliegue de salas con arquitectura SFU (Selective Forwarding Unit) para transmisión fluida de video y audio optimizada para redes móviles inestables.
Control dinámico de silenciamiento de micrófonos, asignación de turnos de palabra y oradores principales para evitar el caos típico de asambleas numerosas.
3. Motor de Quórum y Votación por Coeficiente
Registro algorítmico de asistencia con ponderación por coeficiente de propiedad horizontal hasta 4 decimales.
Publicación instantánea de resultados gráficos para los asambleístas.
4. Gestión de Poderes y Acreditación Documental
Pipeline de subida, validación de tipos MIME y procesamiento de poderes notariales mediante multer.

💡 El Viaje de Creación (Founder Journey)
RoLEMeet no es un proyecto de laboratorio; es el resultado de más de 435 días de desarrollo continuo, pruebas en asambleas reales y evolución técnica.
Filosofía de Producto: Diseñar una herramienta que una persona de 80 años pueda operar desde su teléfono móvil sin frustración, al tiempo que le entrega al revisor fiscal y al administrador un soporte jurídico inalterable.
Modelo Operativo: Arquitectura moderna basada en microservicios, APIs desacopladas y servicios de tiempo real en la nube.

👨‍💻 Autor & Arquitectura de Producto
Jean Michell Leguizamón Romero
Magíster en Gerencia Estratégica de Mercadeo | Fundador y Desarrollador de Producto
LinkedIn
Sitio Oficial RoLEMeet
Contacto: lrreunionesyasambleas@gmail.com