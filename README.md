# SpringBootUsingSpringSecurity-Jwt
Spring Boot + Spring Security {In Memory Authentication} + JWT {JSON Web Token} + Rest

> **###1. Technologies**
* Spring Boot 1.3.5.RELEASE {using parent}
* Spring Boot Security 1.3.5.RELEASE {using parent}
* jjwt 0.9.0 {io.jsonwebtoken}
* json-path {com.jayway.jsonpath}

> **###2. To Run this project locally**
* $ git clone https://github.com/AkashChauhanSoftEngi/SpringBootUsingSpringSecurity-Jwt
* $ tomcat {Embedded}

> **###3.  Access** 
* http://localhost:8080/login
* http://localhost:8080/users

> **###4. Important things to keep in mind**
* JWT: Java Web Tokens
* JWT is split into three majot parts
  1. Header {"typ": "JWT", "alg": "HS256"}
  2. Payload{real message/data}{"username":"abc", "password":"xyz"}
  3. Signature{merge Header and Payload, and Encoded it with Signature}
* Format of the token {3 parts}
  - Header.Payload.Signatuer
  - each part is base64
* Claims: Security Information
* JWT is just to create and communicate through token.
  - whereas Oauth is like Security framework, like when you install app on your phone
  - Your phone, give your secure information to third party or client to make changes on your machine
* Even the same token can be used for accessing multiple web sites
* Reference		: https://www.youtube.com/watch?v=oXxbB5kv9OA
			: https://www.youtube.com/watch?v=-HYrUs1ZCLI&t=29s
			: https://github.com/DylanMeeus/springboot_jwt_blog
* Create JWT	  	: http://jwtbuilder.jamiekurtz.com/
* Verify JWT	  	: https://jwt.io/
* Decode base64 	: https://www.base64decode.org/

> **###5. JWT Work Flow**
* First login to create and receive a token from the response header{if added there}
* We can understand this whole flow in 3 steps
 	A) To create this token, there are few tasks at server side need to be done
    		- If using spring security and AuthenticationManagerBuilder, then verify user credentials
    		- If user exist in the DB, then move to next step to create token
    		- Create New token using user credentials
    		- Add this token to response header and return
    		- If user does not exist then throw error, user does not exist
  	B) Now you can send a request with this Authorize token in the desired request Header
  	C) When you hit any other API using this token, there are few tasks at server side need to be done
    		- Validate this token
    		- if valid then give access to resource
    		- if not valid then give access denied error
  
> **###6. Classes/Interfaces/Methods involved**
* authenticationManager() from WebSecurityConfigurerAdapter to set AuthenticationManager
* AuthenticationManager gonna manage all authentication work internally
* Two methods from AbstractAuthenticationProcessingFilter, need to override
	1- attemptAuthentication() to populate Authentication interface{username, isAuthenticated}
   	2- successfulAuthentication to create token using user credentials
* When Authenticating any other API except /login, then need to populate Authentication interface again by the implementation
* And then set this Authentication to the current context

