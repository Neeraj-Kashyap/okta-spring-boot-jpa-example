# Spring Boot + JPA and PostgreSQL

This example is a resource server using Spring Boot and Spring Data JPA. It also implements group-based authorization using Okta and OAuth 2.0.

Please read [Build a Basic App with Spring Boot and JPA using PostgreSQL](https://developer.okta.com/blog/2018/12/13/build-basic-app-spring-boot-jpa) to see how this app was created.

**Prerequisites:** [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

> [Okta](https://developer.okta.com/) has Authentication and User Management APIs that reduce development time with instant-on, scalable user infrastructure. Okta's intuitive API and expert support make it easy for developers to authenticate, manage, and secure users and roles in any application.

* [Getting Started](#getting-started)
* [Links](#links)
* [Help](#help)
* [License](#license)

## Getting Started

To install this example application, run the following commands:

```bash
git clone https://github.com/oktadeveloper/okta-spring-boot-jpa-example.git
cd okta-spring-boot-jpa-example
```

This will get a copy of the project installed locally. To install all of its dependencies and start the app, run:
 
```bash
./gradlew bootRun
```

This will likely fail. You need to configure a PostgreSQL database with the following settings for everything to work out-of-the-box.

    url: "jdbc:postgresql://localhost:5432/springbootjpa"
    username: oktatutorial
    password: abcd1234

### Create an Application in Okta

You will need to [create an OpenID Connect Application in Okta](https://developer.okta.com/blog/2018/09/26/build-a-spring-boot-webapp#set-up-okta-for-oauth-20-single-sign-on) to get your values to perform authentication. 

Log in to your Okta Developer account (or [sign up](https://developer.okta.com/signup/) if you don’t have an account) and navigate to **Applications** > **Add Application**. Click **SPA**, click **Next**, and give the app a name you’ll remember. Click **Done** and copy the `clientId` into `src/main/resources/application.yml`. 

```yaml                            
okta:  
  oauth2: 
    issuer: https://{yourOktaDomain}/oauth2/default  
    clientId: {yourClientId}  
    scope: openid profile email
    rolesClaim: groups   
```

**NOTE:** The value of `{yourOktaDomain}` should be something like `dev-123456.oktapreview`. Make sure you don't include `-admin` in the value!

After modifying this file, restart your app and you should be able to authenticate with Okta.

## Links

This example uses [Okta's Spring Boot Starter](https://github.com/okta/okta-spring-boot).

## Help

Please post any questions as comments on the [blog post](https://developer.okta.com/blog/2018/12/13/build-basic-app-spring-boot-jpa), or visit our [Okta Developer Forums](https://devforum.okta.com/).

## License

Apache 2.0, see [LICENSE](LICENSE).
