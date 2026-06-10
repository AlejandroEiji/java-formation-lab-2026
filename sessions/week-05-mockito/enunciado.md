# Enunciado — Week 05: Mockito (Buenas Prácticas)

## Contexto del reto

**Indra Payments** tiene un `PaymentService` que depende de tres colaboradores externos: `PaymentGateway` (llamada HTTP real), `FraudDetector` (servicio ML externo) y `AuditLogger` (escribe en base de datos). Los tests actuales arrancan el contexto completo y son lentos (>30 segundos). Tu tarea es reemplazarlos con tests unitarios rápidos usando Mockito.

## Lo que debes implementar

1. Escribe tests unitarios para `PaymentService.processPayment(PaymentRequest)` usando `@ExtendWith(MockitoExtension.class)`.
2. Mockea `PaymentGateway`, `FraudDetector` y `AuditLogger`.
3. Cubre los escenarios:
   - Pago aprobado: gateway retorna `APPROVED`, fraude no detectado → retorna `PaymentResult.SUCCESS`
   - Fraude detectado: `FraudDetector` retorna `true` → lanzar `FraudulentPaymentException` y **no** llamar al gateway
   - Gateway falla: lanza `GatewayException` → `PaymentService` debe propagar como `PaymentProcessingException`
4. Usa `ArgumentCaptor` para verificar que `AuditLogger` recibió el `PaymentRequest` correcto en el escenario de éxito.

## Restricciones técnicas (para todos)

- Usar `@Mock` y `@InjectMocks`, no `Mockito.mock()` manualmente.
- No usar `@SpringBootTest` — estos deben ser tests unitarios puros.
- No verificar con `verify()` interacciones que ya están implícitas en el resultado del test.
- **Criterio no funcional (calidad)**: cada test debe poder leerse como una especificación — el nombre del método describe el escenario y el resultado esperado.

## Criterio de aceptación del PR

- [ ] 3 escenarios cubiertos con tests independientes
- [ ] `ArgumentCaptor` usado correctamente en el escenario de éxito
- [ ] Sin `@SpringBootTest` ni contexto completo
- [ ] Sin `verify()` redundantes (que no agregan valor al test)
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar un test con `@Spy` para verificar que `PaymentService` llama a un método auxiliar propio.
- Usar `BDDMockito` (`given/when/then`) en lugar de `when/thenReturn` para mayor legibilidad.
