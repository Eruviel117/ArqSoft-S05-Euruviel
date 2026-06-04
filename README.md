# Tecnológico de Software
- **Arquitectura de Software**
- **Alumno:** Euruviel Marquez Martinez
- **Docente:** Jorge Javier Pedrozo Romero
- **Fecha:** 04/06/2026
- **Actividad:** Actividad #14 – Práctica .NET: Implementar MVC con ASP.NET Core

---

## Descripción

**CitasMédicas** es una aplicación web desarrollada con **ASP.NET Core MVC** que permite gestionar un sistema de citas médicas. Permite visualizar pacientes registrados, médicos disponibles y la agenda completa de citas, con filtro por paciente.

El proyecto aplica el patrón **repositorio con interfaces**, separando la lógica de acceso a datos de los controladores mediante inyección de dependencias.

---

## Arquitectura

El proyecto sigue una estructura **MVC con capa de repositorios**:

```

Citas_App/
├── Controllers/
│   ├── HomeController.cs
│   ├── PacienteController.cs
│   ├── MedicoController.cs
│   └── CitaController.cs
│
├── Interfaces/
│   ├── IPacienteRepository.cs
│   ├── IMedicoRepository.cs
│   └── ICitaRepository.cs
│
├── Repositories/
│   ├── JsonPacienteRepository.cs
│   ├── JsonMedicoRepository.cs
│   └── JsonCitaRepository.cs
│
├── Models/
│   ├── Paciente.cs
│   ├── Medico.cs
│   ├── Cita.cs
│   └── CitaJson.cs
│
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
│
└── data/
    ├── pacientes.json
    ├── medicos.json
    └── citas.json

```
