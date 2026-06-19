# Tecnológico de Software
- **Arquitectura de Software**
- **Alumno:** Euruviel Marquez Martinez
- **Docente:** Jorge Javier Pedrozo Romero
- **Fecha:** 19/06/2026
- **Actividad:** Actividad #22 – Práctica .NET: API REST con ASP.NET Core Web API

---

## Descripción

**CitasMédicas** es una aplicación web desarrollada con **ASP.NET Core MVC** y extendida con una **API REST** construida sobre una arquitectura hexagonal (Ports & Adapters). Permite gestionar un sistema de citas médicas tanto desde una interfaz web (MVC) como desde cualquier cliente HTTP (Postman, PowerShell, aplicación móvil, navegador).

El proyecto demuestra cómo la arquitectura hexagonal permite **agregar un nuevo cliente** (la API REST) sin modificar el dominio ni la infraestructura existente, únicamente añadiendo una capa de servicios de aplicación y un nuevo proyecto de presentación.

---

## Arquitectura

El proyecto sigue una estructura **hexagonal multi-proyecto** con cinco capas:

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
├── CitasApp.Application/      
│   └── Services/
│       ├── PacienteService.cs
│       ├── MedicoService.cs
│       └── CitaService.cs
│
├── CitasApp.Web/              
│   ├── Controllers/
│   ├── Views/
│   └── data/
│
└── CitasApp.Api/              
    ├── Controllers/
    │   ├── PacientesController.cs
    │   ├── MedicosController.cs
    │   ├── CitasController.cs
    │   └── CalculadoraController.cs
    ├── data/
    │   ├── pacientes.json
    │   ├── medicos.json
    │   └── citas.json
    └── Program.cs
```
