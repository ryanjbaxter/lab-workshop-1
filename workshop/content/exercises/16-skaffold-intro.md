**Skaffold**

*   [Skaffold](https://github.com/GoogleContainerTools/skaffold) is a command line tool that facilitates continuous development for Kubernetes applications
*   Simplifies the development process by combining multiple steps into one easy command
*   Provides the building blocks for a CI/CD process


To check your version of Skaffold.
```execute-1
skaffold version
```



### 
**Adding Skaffold YAML**



*   Skaffold is configured using…you guessed it…another YAML file
*   We create a YAML file `skaffold.yaml` in the root of the project


```editor:append-lines-to-file
file: ~/demo/skaffold.yaml
text: |
        apiVersion: skaffold/v2beta12
        kind: Config
        metadata:
          name: k-s-demo-app--
        build:
          artifacts:
          - image: YourImage
            buildpacks:
              builder: docker.io/paketobuildpacks/builder:base
              dependencies:
                paths:
                - src
                - pom.xml
        deploy:
          kubectl:
            manifests:
            - k8s/deployment.yaml
            - k8s/service.yaml
            - k8s/ingress.yaml
```


Now, source your host from your lab environment and add to your `ingress.yaml`. (This is not necessary outside of this lab).
```execute-1
 sed "s/YourImage/{{ registry_host }}\/apps\/demo/g" skaffold.yaml -i
```

Take a peek at your file to verify your image populted.
```editor:select-matching-text
file: ~/demo/skaffold.yaml
text: "image" 
```

The `builder` is the same one used by Spring Boot when it builds a container from the build plugins (you would see it logged on the console when you build the image). Instead of the `buildpacks` builder you could use the `custom` one (with the same `dependencies`):


```
   custom:
      buildCommand: ./mvnw spring-boot:build-image -D spring-boot.build-image.imageName=$IMAGE && docker push $IMAGE
```



