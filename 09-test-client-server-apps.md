# Test Client Server Applications

- Test clients (integration) by mocking remote services
  ![client test](assets/client-test.png)

- Test servers (integration) by mocking client calls
  ![server test](assets/server-test.png)

- Example using Spring MockMvc

```java
@WebMvcTest
@ContextConfiguration(classes = RestController.class)
class RestControllerTest {
    // Allows to mock the client
    @Autowired
    private MockMvc mockMvc;
    @Autowired
    private ObjectMapper objectMapper;
    @Test
    void testGetAllObjects() throws Exception {
        List<Object> expectedResultList = new ArrayList<Object>(); // add the expected objects here
        // Performs a GET request on the actual server and checks
        // that the response code is 200 (OK)
        ResultActions request = mockMvc.perform(get("/objects")).andDo(print()).andExpect(status().isOk());
        // Response as (json) string
        String response = request.andReturn().getResponse().getContentAsString();
        // Map response to Java objects
        List<Object> actualResultList =
        Arrays.stream(objectMapper.readValue(response, Object[].class)).collect(Collectors.toList());
        // Compare expected and actual response
        assertThat(actualResultList).containsExactlyInAnyOrderElementsOf(expectedResultList);
    }
}
```
