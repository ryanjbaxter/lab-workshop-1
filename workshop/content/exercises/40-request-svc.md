Delete previous implementation of the `hello` method in `K8sDemoAppApplication.java`

```execute-1
 sed -i '19d' ~/demo/src/main/java/com/example/demo/K8sDemoAppApplication.java
```


Modify the `hello` method of `K8sDemoApplication.java` to make a request to the new service.

First add the appropriate imports for `RestTemplate` and `RestTemplateBuilder`.
```editor:insert-lines-before-line
file: ~/demo/src/main/java/com/example/demo/K8sDemoAppApplication.java
line: 8
text: |
		import org.springframework.web.client.RestTemplate;
		import org.springframework.boot.web.client.RestTemplateBuilder;

```

Instantiate a new `RestTemplate` instance.


```editor:insert-lines-before-line
file: ~/demo/src/main/java/com/example/demo/K8sDemoAppApplication.java
line: 14
text: |
		private RestTemplate rest = new RestTemplateBuilder().build();

```

Finally use the `RestTemplate` to make a `GET` request to the `k8s-workshop-name-service`.

```editor:insert-lines-before-line
file: ~/demo/src/main/java/com/example/demo/K8sDemoAppApplication.java
line: 22
text: |
		String name = rest.getForObject("http://k8s-workshop-name-service", String.class);
		return "Hola " + name;

```




*   Notice the hostname of the request we are making matches the service name in [our service.yaml file](https://github.com/ryanjbaxter/k8s-spring-workshop/blob/master/name-service/kustomize/base/service.yaml#L7)



---
