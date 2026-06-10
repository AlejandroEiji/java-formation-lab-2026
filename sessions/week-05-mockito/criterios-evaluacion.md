# Criterios de evaluación — Week 05

## Checklist del reviewer

### Mocks
- [ ] `@Mock` y `@InjectMocks` usados (no `Mockito.mock()` manual)
- [ ] `@ExtendWith(MockitoExtension.class)` presente
- [ ] Sin `@SpringBootTest`

### Escenarios
- [ ] Test: pago aprobado → `PaymentResult.SUCCESS`
- [ ] Test: fraude detectado → `FraudulentPaymentException` y gateway no invocado
- [ ] Test: gateway falla → `PaymentProcessingException`

### ArgumentCaptor
- [ ] `ArgumentCaptor` usado para verificar el payload al `AuditLogger`
- [ ] El captor verifica datos relevantes del `PaymentRequest`

### Calidad de tests
- [ ] Sin `verify()` redundantes que no agregan información
- [ ] Nombres de tests descriptivos del escenario y resultado
- [ ] `mvn verify` en verde

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Tests con mocks básicos, algunos verify redundantes | 3 escenarios, ArgumentCaptor correcto | BDDMockito, tests como especificaciones, sin ruido | Identifica qué NO mockear, propone tests de integración para los contratos |
