# Tecnológico de Software
- **Arquitectura de Software**
- **Alumno:** Euruviel Marquez Martinez
- **Docente:** Jorge Javier Pedrozo Romero
- **Fecha:** 07/07/2026
- **Actividad:** Actividad #29 – Práctica .NET: Diagramas como código

---

## Descripción

**CitasMédicas** es una aplicación web desarrollada con **ASP.NET Core MVC** refactorizada a **Arquitectura Hexagonal (Ports & Adapters)**. Permite gestionar un sistema de citas médicas visualizando pacientes registrados, médicos disponibles y la agenda completa de citas.

El proyecto demuestra cómo la arquitectura hexagonal permite **intercambiar la fuente de datos** (JSON, CSV o SQLite) sin modificar los controladores ni el dominio, simplemente cambiando el adaptador activo en `Program.cs`.

---

## Arquitectura

El proyecto sigue una estructura **hexagonal multi-proyecto**:


```
CitasApp.sln
├── CitasApp.Domain/
│   ├── Models/
│   │   ├── Paciente.cs
│   │   ├── Medico.cs
│   │   ├── Cita.cs
│   │   └── CitaJson.cs
│   └── Interfaces/
│       ├── IPacienteRepository.cs
│       ├── IMedicoRepository.cs
│       └── ICitaRepository.cs
│
├── CitasApp.Infrastructure/
│   └── Repositories/
│       ├── JsonPacienteRepository.cs
│       ├── JsonMedicoRepository.cs
│       ├── JsonCitaRepository.cs
│       ├── CsvPacienteRepository.cs
│       ├── CsvMedicoRepository.cs
│       ├── CsvCitaRepository.cs
│       ├── SqlitePacienteRepository.cs
│       ├── SqliteMedicoRepository.cs
│       └── SqliteCitaRepository.cs
│
└── CitasApp.Web/
    ├── Controllers/
    │   ├── HomeController.cs
    │   ├── PacienteController.cs
    │   ├── MedicoController.cs
    │   └── CitaController.cs
    ├── Views/
    │   ├── Paciente/
    │   │   ├── Index.cshtml
    │   │   └── Detalle.cshtml
    │   ├── Medico/
    │   │   ├── Index.cshtml
    │   │   └── Detalle.cshtml
    │   └── Cita/
    │       ├── Index.cshtml
    │       └── PorPaciente.cshtml
    └── data/
        ├── pacientes.json
        ├── medicos.json
        ├── citas.json
        ├── pacientes.csv
        ├── medicos.csv
        ├── citas.csv
        └── citasapp.db
```

---

## Funcionalidades

| Funcionalidad | Descripción |
|---|---|
| Lista de pacientes | Tabla con nombre, email y teléfono de cada paciente |
| Detalle de paciente | Información completa con link a sus citas |
| Lista de médicos | Tabla con nombre, especialidad y número de licencia |
| Detalle de médico | Información completa del médico |
| Agenda de citas | Tabla con fecha, hora, paciente, médico, motivo y estado |
| Citas por paciente | Filtro de citas de un paciente específico |
| Intercambio de adaptador | Cambio de fuente de datos sin modificar controllers ni dominio |

---

## Tecnologías utilizadas

| Tecnología | Versión | Uso |
|---|---|---|
| C# | 13 | Lenguaje principal |
| ASP.NET Core MVC | .NET 10 | Framework web |
| JSON | — | Adaptador de persistencia A |
| CSV | — | Adaptador de persistencia B |
| SQLite | 10.0.9 | Adaptador de persistencia C |
| Git + GitHub | — | Control de versiones |

---

## Adaptadores de datos

El sistema soporta 3 fuentes de datos intercambiables desde `Program.cs`:

| Bloque | Adaptador | Archivos |
|---|---|---|
| Bloque A | JSON | `pacientes.json`, `medicos.json`, `citas.json` |
| Bloque B | CSV | `pacientes.csv`, `medicos.csv`, `citas.csv` |
| Bloque C | SQLite | `citasapp.db` |

Para cambiar de adaptador solo se descomenta el bloque correspondiente en `Program.cs`. **Los controllers y el dominio nunca cambian.**

---

## Patrones y principios aplicados

| Principio | Aplicación |
|---|---|
| **Arquitectura Hexagonal** | Domain, Infrastructure y Web separados en proyectos independientes |
| **Ports & Adapters** | Las interfaces son los puertos; los repositorios JSON/CSV/SQLite son los adaptadores |
| **Patrón Repositorio** | Interfaces `IPacienteRepository`, `IMedicoRepository`, `ICitaRepository` desacoplan el acceso a datos |
| **Inyección de dependencias** | Repositorios registrados en `Program.cs` como `AddScoped` |
| **SRP** — Single Responsibility | Cada controller maneja una sola entidad |
| **DIP** — Dependency Inversion | Los controllers dependen de interfaces, no de implementaciones concretas |

---

## Vistas arquitectónicas

| Vista | Descripción |
|---|---|
| **Lógica** | Módulos: Gestión de Pacientes, Gestión de Médicos, Gestión de Citas |
| **Desarrollo** | Tres proyectos: Domain (modelos e interfaces), Infrastructure (repositorios), Web (controllers y vistas) |
| **Procesos** | Petición HTTP → Controller → Interface (Port) → Repositorio (Adapter) → Fuente de datos → View |

---

## Capturas de pantalla de Paciente, Medico y Citas del Bloque A





<img width="1365" height="767" alt="Captura de pantalla 2026-06-12 183801" src="https://github.com/user-attachments/assets/c5da8449-097a-4359-8b5a-0b4562276821" />





<img width="1365" height="767" alt="Captura de pantalla 2026-06-12 183806" src="https://github.com/user-attachments/assets/6f46b60f-55bc-4501-b270-6ae1f2011bef" />




<img width="1365" height="756" alt="Captura de pantalla 2026-06-12 183810" src="https://github.com/user-attachments/assets/7681c3d5-4a16-40b8-8089-76685583ad0d" />



## Capturas de pantalla de Paciente, Medico y Citas del Bloque B


<img width="1365" height="767" alt="Captura de pantalla 2026-06-12 183707" src="https://github.com/user-attachments/assets/768d6fc1-945e-4136-aaae-f3ce5376e3c6" />



<img width="1365" height="767" alt="Captura de pantalla 2026-06-12 183718" src="https://github.com/user-attachments/assets/64c9384b-0917-46c8-a150-451dcc1fd320" />



<img width="1365" height="767" alt="Captura de pantalla 2026-06-12 183723" src="https://github.com/user-attachments/assets/73489bb8-f93b-440f-aaae-b9e00f119d98" />


---

## Diagramas de arquitectura

Los diagramas UML y C4 del proyecto están documentados como código Mermaid en:

 [Ver diagramas de arquitectura](arquitectura.md)

Incluye:
- Diagrama de clases — Paciente, Medico, Cita, interfaces y patrones GoF
- C4 Nivel 1 — Contexto del sistema
- C4 Nivel 2 — Contenedores
- C4 Nivel 3 — Componentes dentro de CitasApp.Api
