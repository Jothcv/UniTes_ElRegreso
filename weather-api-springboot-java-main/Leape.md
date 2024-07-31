# Cosas aprendidas
## ¿Qué es Mockito?
Mockito es una herramienta super útil en Java para hacer pruebas unitarias. Te permite crear objetos simulados (llamados mocks) para verificar que tus componentes de aplicación funcionen como esperas. Es genial para probar partes específicas de tu código sin tener que depender de los demás componentes.

## ¿Para qué sirve Mockito?
Creación de Mocks: Crea objetos simulados que imitan el comportamiento de objetos reales.
Verificación de Interacciones: Comprueba que los métodos en los mocks se llamaron con los parámetros que esperabas.
Configuración de Respuestas: Define cómo deben responder los mocks a ciertos métodos.
## Cómo Usar Mockito
Añadir Dependencia
Primero, añade Mockito a tu proyecto. Si usas Maven, agrégalo a tu archivo pom.xml:

<dependency>
<groupId>org.mockito</groupId>
<artifactId>mockito-core</artifactId>
<version>4.10.0</version>
<scope>test</scope>
</dependency>
Crear un Mock
Para crear un mock, usa el método Mockito.mock():


MyClass myMock = Mockito.mock(MyClass.class);
Configurar Comportamiento
Define cómo debe comportarse el mock con Mockito.when():


Mockito.when(myMock.someMethod()).thenReturn(someValue);
Verificar Interacciones
Asegúrate de que los métodos en el mock fueron llamados con los parámetros correctos:

Mockito.verify(myMock).someMethod();
Usar @Mock y @InjectMocks
Para facilitar la configuración en tus pruebas con JUnit, puedes usar anotaciones:


@Mock
private MyDependency myDependency;

@InjectMocks
private MyService myService;
### Ejemplo Completo

import static org.mockito.Mockito.*;

public class MyServiceTest {

    @Mock
    private MyDependency myDependency;

    @InjectMocks
    private MyService myService;

    @Before
    public void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    public void testServiceMethod() {
        when(myDependency.getData()).thenReturn("mocked data");

        String result = myService.processData();
        
        verify(myDependency).getData();
        assertEquals("processed mocked data", result);
    }
}