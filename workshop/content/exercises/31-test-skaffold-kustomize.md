

### 
**Testing Skaffold + Kustomize**



*   If you run your normal `skaffold` commands it will use the deployment configuration from `kustomize/base`


```execute-1
skaffold dev --port-forward

```



*   If you want to test out the QA deployment run the following command to activate the QA profile


```execute-1
skaffold dev -p qa --port-forward
```


Be sure to kill the `skaffold` process before continuing

```terminal:interrupt
session: 1
```


---


