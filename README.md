# GitHub Package Registry + Maven Example

This project shows how add a maven dependency stored in the brand new  [GitHub Package Registry](https://github.com/features/package-registry).  
For now this feature is in beta. To use it, you have to [sign up for the beta](https://github.com/features/package-registry/signup).

The package is released [here](https://github.com/TobseF/HelloMaven/packages).  

To deploy a package by your own and setup a [GitHub Actions](https://github.com/features/actions) CI, check the [HalloMaven](https://github.com/TobseF/HelloMaven/) project.   

You can find more info for Package Registry in the official GitHub doc:  
📚 [Configuring Apache Maven for use with GitHub Package Registry](https://help.github.com/en/articles/configuring-apache-maven-for-use-with-github-package-registry)

## Add dependency
The dependency is added like every other in maven in the `pom.xml`:

```xml
<dependency>
    <groupId>github.tobsef</groupId>
    <artifactId>hello-maven</artifactId>
    <version>1.2.1</version>
</dependency>
```
To point maven to the repo, we also have to specify the `repositoriy` in the `pom.xml`.
```xml
<repositories>
    <repository>
        <id>github</id>
        <name>GitHub TobseF Apache Maven Packages</name>
        <url>https://maven.pkg.github.com/TobseF/HelloMaven</url>
        <releases><enabled>true</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
    </repository>
</repositories>
```
## Enable authentication
The registry access is available through the GitHub api which is protected by an authorisation.
So you have ro add the credentials to the Package Registry to your global `settings.xml`:  
`USER_HOME\.m2\settings.xml`

``` xml
<servers>
    <server>
        <id>github</id>
        <username>YOUR_USERNAME</username>
        <password>YOUR_AUTH_TOKEN</password>
    </server>
</servers>
```
Replace the `YOUR_USERNAME` with your GitHub login name.  
Replace the `YOUR_AUTH_TOKEN` with a generated GitHub personal access token:  
_GitHub_ > _Settings_ > _Developer Settings_ > _Personal access tokens_ > _Generate new token_:   
The token needs at least the `read:packages` scope.
Otherwise you will get a `Not authorized` exception.


### Setup your own
If you want to use the Package Registry in your own project, make sure its activated.
Therefore check your project package site:  
https://github.com/YOUR_NAME/YOUR_PROJECT/packages
