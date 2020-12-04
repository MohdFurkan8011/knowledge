#### Exception

​	We are handling exception using annotation.

1. **@ResponseStatus** for exception status and contomized message.

   The **@ResponseStatus** annotation can be used on methods and exception classes. It can be configured with a status code which would be applied to the HTTP response.

   ```java
   @ResponseStatus(value = HttpStatus.NOT_FOUND, reason = "User Not found")
   public class UserNotFoundException extends RuntimeException {
   }
   ```

2. **@ExceptionHandler**

   - **Controller level**  -

     This approach has a major drawback. The @ExceptionHandler annotated method is only active for that particular controller, not globally for the entire application. Of course, adding this to every controller makes it not well suited for a general exception handling mechanism.

     ```java
     @RestController
     public class FooController{
     	//...
     	@ExceptionHandler({ CustomException1.class, CustomException2.class })
     	public void handleException() {
         	//
     	}
     }
     ```

   - **Globally level** -

     Globally level is acheived by @ControllerAdvice or @RestControllerAdvice

3. **@ControllerAdvice**-

   Through @ControllerAdvice we acheive exception handling globally. @ExceptionHandler is used with @ControllerAdvice.

   ```java
   @ControllerAdvice
   public class AppExceptionHandler extends ResponseEntityExceptionHandler {
   
       @ExceptionHandler(UserNotFound.class)
       public ResponseEntity<Object> handleUserNotFoundException(
           UserNotFoundException ex, WebRequest request) {
   
           Map<String, Object> body = new LinkedHashMap<>();
           body.put("timestamp", LocalDateTime.now());
           body.put("message", "City not found");
   
           return new ResponseEntity<>(body, HttpStatus.NOT_FOUND);
       }
       
       @Override
       protected ResponseEntity<Object> handleMethodArgumentNotValid(
           MethodArgumentNotValidException ex, HttpHeaders headers, 
           HttpStatus status, WebRequest request) {
   
           Map<String, Object> body = new LinkedHashMap<>();
           body.put("timestamp", LocalDate.now());
           body.put("status", status.value());
   
           List<String> errors = ex.getBindingResult()
                   .getFieldErrors()
                   .stream()
                   .map(x -> x.getDefaultMessage())
                   .collect(Collectors.toList());
   
           body.put("errors", errors);
   
           return new ResponseEntity<>(body, HttpStatus.BAD_REQUEST);
       }
   
   }
   ```

   

4. **@RestControllerAdvice**

   For reset controller, By default `@RestControllerAdvice` is applicable to the whole application but you can restrict it to a specific package, class or annotation.

   ```java
   @RestControllerAdvice(basePackages = "my.package")
   @RestControllerAdvice(basePackageClasses = MyController.class)
   @RestControllerAdvice(assignableTypes = MyController.class)
   @RestControllerAdvice(annotations = RestController.class)
   ```

   

   ```sql
   @RestControllerAdvice
   public class AppExceptionHandler {
   
       @ResponseBody
       @ExceptionHandler(value = ValidationException.class)
       public ResponseEntity<?> handleException(ValidationException exception) {
           return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(exception.getMsg());
       }
   }
   ```

5. **ResponseStatusException** (Spring 5 and above)

   - Excellent for prototyping: We can implement a basic solution quite fast.
   - One type, multiple status codes: One exception type can lead to multiple different responses. **This reduces tight coupling compared to the @ExceptionHandler**
   - We won't have to create as many custom exception classes.

   ```java
   throw new ResponseStatusException(
              HttpStatus.NOT_FOUND, "Foo Not Found", exc);
   ```

   



`Note-`

As you can see, Spring provides us with different options to do exception handling in our apps. You can use one or a combination of them based on your needs. Here is the rule of thumb:

- For custom exceptions where your status code and message are fixed, consider adding `@ResponseStatus` to them.
- For exceptions where you need to do some logging, use `@RestControllerAdvice` with `@ExceptionHandler`. You also have more controller over your response text here.
- For changing the behavior of the default Spring exception responses, you can extend the `ResponseEntityExceptionHandler` class.