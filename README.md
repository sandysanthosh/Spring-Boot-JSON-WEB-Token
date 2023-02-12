# Spring-Boot-JSON-WEB-Token

Spring Boot REST API that implements JWT (JSON Web Token) authentication using a bearer token and Test it in Postman


```

@RestController
@RequestMapping("/api")
public class ExampleController {

  @GetMapping("/protected")
  public ResponseEntity<String> protectedEndpoint(@RequestHeader("Authorization") String token) {
    if (!isTokenValid(token)) {
      return ResponseEntity.status(HttpStatus.UNAUTHORIZED).build();
    }

    return ResponseEntity.ok("Access granted to protected endpoint");
  }

  private boolean isTokenValid(String token) {
    if (token == null || !token.startsWith("Bearer ")) {
      return false;
    }

    String jwt = token.substring(7);

    try {
      Jwts.parser().setSigningKey("secret").parseClaimsJws(jwt);
      return true;
    } catch (Exception ex) {
      return false;
    }
  }
}


```

In this example, a user must pass a bearer token in the Authorization header of their request to access the /api/protected endpoint. The isTokenValid method is used to validate the token, which is done by checking if it starts with the Bearer keyword, and then attempting to parse the JWT using the secret signing key. If the token is invalid, the method returns false, which results in a 401 Unauthorized response being returned to the user. If the token is valid, the method returns true, and the user is granted access to the protected endpoint.

#### To test this in Postman, you can follow these steps:

* Create a new request in Postman

* Choose the GET method

* Enter the URL of your endpoint (e.g. http://localhost:8080/api/protected)

* In the Headers tab, add a new header with the key Authorization and the value Bearer <your-jwt-token>

* Send the request

If the token is valid, you should receive a 200 OK response with the message Access granted to protected endpoint. If the token is invalid, you should receive a 401 Unauthorized response.



