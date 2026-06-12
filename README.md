# Tecnológico de Software
- **Arquitectura de Software**
- **Alumno:** Euruviel Marquez Martinez
- **Docente:** Jorge Javier Pedrozo Romero
- **Fecha:** 12/06/2026
- **Actividad:** Actividad #18 – Práctica .NET: Arquitectura Hexagonal

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
