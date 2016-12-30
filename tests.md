# Writing tests in James

## AssertJ framework

When writing a test within James, we use the Junit framework.

However, we find the Junit Asserts poor. Thus we decided to use [AssertJ](http://joel-costigliola.github.io/assertj/).

AssertJ have assertions, for java-8, for collections, for raw types and Strings.

Here is the syntax :

```java
import static org.assertj.core.api.Assertions.assertThat;

class MyTest {
    private Testee testee;
    
    @Before
    public void setUp() {
        testee = new Testee();
    }
    
    @Test
    public void demonstrateCollections() {
        // Given
        String data = "";
        
        // When
        Collection collection = testee.generateCollection(data);
        
        // Then
        assertThat(collection).isEmpty();
        assertThat(collection).containsOnly(a, b, c); //Look for the elements but nut the order
        assertThat(collection).containsExactly(a, b, c);
    }
    
    
    @Test
    public void demonstrateBoolean {
        boolean bool = testee.IsItRainaing();
        
        assertThat(bool).isFalse();
        assertThat(bool).isTrue();
    }
    
    
    @Test
    public void demonstrateObjects {
        String aString = testee.getLocation();
        
        assertThat(aString).isEqualTo("abcd");
        assertThat(aString).startsWith("abc");
    }
}
```

The assertJ page have many more example.

## Testing rules

Here are some rules we follow for the tests :

 - There name should be of the form : 
 
 ```
 [method] Should [Action] When [Condition]
```

It aims at making the test easier to read. It also declare the purpose of the test.

 - A test should be simple. Avoid "if", "for" and as much computing logic as possible. If not necessary also avoid method extraction. This aims at making tests easier to read.
 
 - Our tests should be short. A few lines ideally.
 
 - We try to cover "corner cases". What happen when the collection is empty ? When it's null ?
 
 - We choosed to test threw the API. We try not to use implementation specific details in our tests. It allows us to easily port the testing suite accross implementations.
 
 - Here we will only write unit tests, but we perform as much integration tests as possible.
