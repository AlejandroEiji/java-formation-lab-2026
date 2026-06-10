# Criterios de evaluación — Week 08

## Checklist del reviewer

### Setup
- [ ] `@WebMvcTest(ProductController.class)` en la clase de test
- [ ] `@MockBean ProductService` presente
- [ ] Sin `@SpringBootTest`, sin contexto de base de datos

### Tests
- [ ] GET con producto existente → 200 + jsonPath correcto
- [ ] GET con producto inexistente → 404
- [ ] POST válido → 201 + header Location
- [ ] POST inválido → 400 con mensaje de error
- [ ] DELETE → 204

### Calidad
- [ ] `jsonPath` usado para verificar campos del body
- [ ] Sin assertions manuales del body como String (usar jsonPath)
- [ ] Tiempo de ejecución < 3s (verificar con `mvn test -Dtest=ProductControllerTest`)
- [ ] `mvn verify` en verde

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| 3/5 tests con @WebMvcTest | 5 tests, jsonPath correcto, <3s | Content-Type, Location header, auth básica | Propone estrategia de testing: qué va en WebMvcTest vs unitario vs integración |
