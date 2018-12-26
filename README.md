# Unchecked Exception 
[![Maven Central](https://img.shields.io/maven-central/v/me.qoomon/unchecked-exceptions.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22me.qoomon%22%20AND%20a%3A%22unchecked-exceptions%22) [![Build Status](https://travis-ci.org/qoomon/unchecked-exceptions-java.svg?branch=master)](https://travis-ci.org/qoomon/unchecked-exceptions-java)

This lib can be used to throw checked exceptions without actually declaring this in your method's head throws clause.

## Methods

Rethrow exception as unchecked exception, without wrapping exception.
```java
  unchecked(exception);
```

Catch and rethrow exception from lambda function as unchecked exception, without wrapping exception.
```java
  unchecked(() -> ...)
```

## Usage Examples
### Try-Catch Block
#### Regular Code 
```java
  import static me.qoomon.UncheckedExceptions.*;

  public class Example {
      
      void example() {
          URL url;
          // code polition with try catch block
          try {
            url = new URL("https:/www.example.org");
          } catch (MalformedURLException e) {
            // ugly exception wrapping
            throw RuntimeException(e); 
          }
          System.out(url);
      }
  }
```
#### Unchecked Exception Code

**or even better**
```java
  import static me.qoomon.UncheckedExceptions.*;

  public class Example {
      
      void example() {
        // get rid of code polition with try catch block
        // and ugly exception wrapping
        URL url = unchecked(() -> new URL("https:/www.example.org"));
        System.out(url);
      }
  }
```
*or*
```java
  import static me.qoomon.UncheckedExceptions.*;

  public class Example {
      
      void example() {
        URL url;
        try {
          url = new URL("https:/www.example.org");
        } catch (MalformedURLException e) {
          // get rid of ugly exception wrapping
          throw unchecked(e);
        }
        System.out(url);
      }
  }
```
### Stream
#### Regular Code 
```java
  
    import static me.qoomon.UncheckedExceptions.*;
  
    public class Example {
        
        void example() {
          Stream.of("https:/www.example.org")
            .map(url -> {
              // code polition with try catch block
              try {
                return new URL(url);
              } catch (MalformedURLException e) {
                // ugly exception wrapping
                throw new RuntimeException(e);
              }
            });
        }
    }
```
#### Unchecked Exception Code
```java
  
    import static me.qoomon.UncheckedExceptions.*;
  
    public class Example {
        
        void example() {
            Stream.of("https:/www.example.org")
                // get rid of code polition with try catch block
                // and ugly exception wrapping
                .map(url -> unchecked(() -> new URL(url)));
            }
    }
```

 
