# Tecnológico de Software
- **Arquitectura de Software**
- **Alumno:** Euruviel Marquez Martinez
- **Docente:** Jorge Javier Pedrozo Romero
- **Fecha:** 26/06/2026
- **Actividad:** Práctica #26 – Práctica .NET: Implementar en C#

---

## Descripción

**CitasMédicas** es una aplicación web desarrollada con **ASP.NET Core Web API** sobre arquitectura hexagonal, extendida con tres patrones de diseño: **Factory**, **Decorator** y **Observer**.

La práctica demuestra cómo estos patrones permiten agregar comportamiento nuevo (logging, selección de repositorio por entorno, notificaciones) **sin modificar el código existente**, cumpliendo con el principio Open/Closed de SOLID.

---


## Arquitectura

El proyecto sigue una estructura **hexagonal multi-proyecto** con cinco capas:


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
    │       ├── ICitaRepository.cs
    │       └── ICitaObserver.cs
    │
    ├── CitasApp.Infrastructure/
    │   ├── Repositories/
    │   │   ├── JsonPacienteRepository.cs
    │   │   ├── MemoriaPacienteRepository.cs
    │   │   ├── LoggingPacienteRepository.cs
    │   │   └── RepositoryFactory.cs
    │   └── Observers/
    │       ├── SmsObserver.cs
    │       └── EmailObserver.cs
    │
    ├── CitasApp.Application/
    │   └── Services/
    │       ├── PacienteService.cs
    │       ├── MedicoService.cs
    │       └── CitaService.cs
    │
    ├── CitasApp.Web/
    │
    └── CitasApp.Api/
        ├── Controllers/
        │   ├── PacientesController.cs
        │   ├── MedicosController.cs
        │   ├── CitasController.cs
        │   └── CalculadoraController.cs
        ├── data/
        └── Program.cs



---

## Patrones implementados

| Patrón | Clase | Descripción |
|---|---|---|
| **Factory** | `RepositoryFactory` | Decide qué repositorio crear según el entorno (Development → JSON, Production → Memoria) |
| **Decorator** | `LoggingPacienteRepository` | Envuelve cualquier repositorio agregando logs en consola sin modificarlo |
| **Observer** | `SmsObserver`, `EmailObserver` | Se notifican automáticamente al confirmar una cita, sin que `CitaService` los conozca directamente |

---

## Funcionalidades

| Funcionalidad | Descripción |
|---|---|
| GET /api/pacientes | Retorna la lista de pacientes en JSON + logs del Decorator en consola |
| GET /api/pacientes/{id} | Retorna el detalle de un paciente + logs del Decorator en consola |
| GET /api/medicos | Retorna la lista completa de médicos en JSON |
| GET /api/medicos/{id} | Retorna el detalle de un médico por ID |
| GET /api/citas | Retorna la agenda completa de citas en JSON |
| GET /api/citas/porpaciente/{id} | Retorna las citas de un paciente específico |
| POST /api/citas/confirmar/{id} | Confirma una cita y dispara notificaciones SMS y EMAIL en consola |
| GET /api/calculadora/sumar | Suma dos números y retorna resultado en JSON |
| GET /api/calculadora/restar | Resta dos números y retorna resultado en JSON |
| GET /api/calculadora/multiplicar | Multiplica dos números y retorna resultado en JSON |
| GET /api/calculadora/dividir | Divide dos números (valida división entre cero) |

---

## Tecnologías utilizadas

| Tecnología | Versión | Uso |
|---|---|---|
| C# | 13 | Lenguaje principal |
| ASP.NET Core Web API | .NET 10 | Framework REST |
| JSON | — | Adaptador de persistencia activo (Development) |
| Memoria | — | Adaptador de persistencia simulado (Production) |
| GitHub | — | Control de versiones |

---

## Vistas arquitectónicas

| Vista | Descripción |
|---|---|
| **Lógica** | Módulos: Gestión de Pacientes (con Factory + Decorator), Gestión de Citas (con Observer) |
| **Desarrollo** | Cinco proyectos: Domain, Application, Infrastructure, Web y Api |
| **Procesos** | Petición HTTP → Controller → Service → LoggingDecorator → Factory → Repositorio → JSON/Memoria |

---

## Capturas de pantalla






<img width="1365" height="763" alt="Captura de pantalla 2026-06-23 184319" src="https://github.com/user-attachments/assets/31622ccb-19de-4eaa-be78-3197962e8e03" />


<img width="1365" height="766" alt="Captura de pantalla 2026-06-23 202916" src="https://github.com/user-attachments/assets/eca74938-d9aa-4782-a10f-54058f193167" />



<img width="1365" height="767" alt="Captura de pantalla 2026-06-23 205715" src="https://github.com/user-attachments/assets/56bce650-1f16-4a55-9164-f6638012034e" />


<img width="1365" height="767" alt="Captura de pantalla 2026-06-23 210124" src="https://github.com/user-attachments/assets/545653e1-c09a-418a-ad58-7194aa53b89e" />


<img width="1365" height="767" alt="Captura de pantalla 2026-06-23 205613" src="https://github.com/user-attachments/assets/d75ceeb8-5d24-4f17-9a56-48acfa51ec7b" />

