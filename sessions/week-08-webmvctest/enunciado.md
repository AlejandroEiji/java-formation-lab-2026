# Enunciado — Week 08: WebMvcTest (Slice Tests)

## Contexto del reto

El `ProductController` expone endpoints REST para gestionar el catálogo de productos. Los tests actuales usan `@SpringBootTest` y levantan la base de datos completa, lo que hace que el pipeline tarde 4 minutos en la fase de test. Tu tarea es reescribirlos como slice tests con `@WebMvcTest`.

## Lo que debes implementar

Con `@WebMvcTest(ProductController.class)` y `@MockBean` para el service:

1. Test: `GET /api/products/{id}` con producto existente → `200` con body correcto (verificar `jsonPath`).
2. Test: `GET /api/products/{id}` con producto inexistente → `404` (service lanza `ProductNotFoundException`).
3. Test: `POST /api/products` con body válido → `201` con `Location` header.
4. Test: `POST /api/products` con body inválido (nombre vacío) → `400` con mensaje de error.
5. Test: `DELETE /api/products/{id}` → `204 No Content`.

## Restricciones técnicas (para todos)

- Usar `@WebMvcTest` — **no** `@SpringBootTest`.
- Usar `@MockBean` para `ProductService` — no instanciar el service real.
- Usar `MockMvc` con `perform/andExpect` — no `RestTemplate`.
- **Criterio no funcional (performance)**: los 5 tests deben ejecutarse en menos de 3 segundos en total.

## Criterio de aceptación del PR

- [ ] 5 tests implementados con `@WebMvcTest`
- [ ] Sin `@SpringBootTest` ni base de datos en los tests
- [ ] `jsonPath` usado para verificar el body de la respuesta
- [ ] Header `Location` verificado en el test de creación
- [ ] Tiempo de ejecución < 3s (reportado en el PR)
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar un test para un endpoint que requiere autenticación básica, usando `MockMvc.with(httpBasic(...))`.
- Verificar el `Content-Type` de la respuesta en todos los tests.
