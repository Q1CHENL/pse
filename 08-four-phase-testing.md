# Four Phase Testing

A flow of events to interact with the SUT

```java
@ExtendWith(MockitoExtension.class)
class EnrollmentServiceTest {
    private static EnrollmentService enrollmentService;
    private Student student;
    private Course courseMock = mock(Course.class);
    @BeforeEach
    void setUp() {
        // Phase 1: Setup
        // 1a) Setup collaborating objects
        enrollmentService = new EnrollmentService();
    }
    @Test
    void testEnrollmentStudentSuccessful() {
        // 1b) Continued setup: Create instance of SUT
        student = new Student();
        // Phase 2: Exercise
        enrollmentService.enroll(student, courseMock);
        // Phase 3: Validate
        assertEquals(...);
        assertTrue(...);
    }
    //...
    @AfterEach
    void tearDown() {
        // Phase 4: Teardown
        reset(courseMock);
    }
}
```
