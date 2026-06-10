# Week 08 — WebMvcTest: Slice Tests de Controllers

**Fecha**: 2026-08-20 · **Paquete**: Spring Web / Testing

## Objetivo

Probar controllers REST con `@WebMvcTest` y `MockMvc` sin levantar el contexto completo de Spring: tests rápidos, enfocados y que no requieren base de datos.

## Contexto técnico

**Brecha QC atacada**: Testing (79%)  
Los tests de controller con `@SpringBootTest` tardan 15–30 segundos. Con `@WebMvcTest` tardan menos de 2. Esta diferencia define si el equipo ejecuta los tests frecuentemente o los evita.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: @SpringBootTest vs @WebMvcTest, diferencia de tiempo |
| 10–45' | Reto: slice tests del controller de pedidos (ver `enunciado.md`) |
| 45–55' | Validación: tests corriendo en <2s, todos los status codes verificados |
| 55–60' | Cierre: `week-08-solution`, qué pertenece a WebMvcTest vs test unitario |
