# tanzu-java-web-app

This is a sample of a Java Spring app that works with Tilt and the Tanzu Application Platform.

## Dependencies
1. [kubectl CLI](https://kubernetes.io/docs/tasks/tools/)
1. [Tilt version >= v0.23.2](https://docs.tilt.dev/install.html)
1. Tanzu CLI and the apps plugin v0.2.0 which are provided as part of [Tanzu Application Platform](https://network.tanzu.vmware.com/products/tanzu-application-platform)
1. A cluster with Tanzu Application Platform, and the "Default Supply Chain", plus its dependencies. This supply chains is part of [Tanzu Application Platform](https://network.tanzu.vmware.com/products/tanzu-application-platform).

## Running the sample

Start the app deployment by running:

```
tilt up
```

You can hit the spacebar to open the UI in a browser. 

- > If you see an "Update error" message like the one below, then just follow the instructions and allow that context:
    ```
    Stop! tap-beta2 might be production.
    If you're sure you want to deploy there, add:
        allow_k8s_contexts('tap-beta2')
    to your Tiltfile. Otherwise, switch k8s contexts and restart Tilt.
    ```

## Tanzu Notes

- [Provistion TAP environment](http://tap-gui.tap-ashumilov-cluster.tapdemo.vmware.com)

- [TAP GUI](http://tap-gui.tap-ashumilov-cluster.tapdemo.vmware.com/)

## Show cluster urls and data

```bash
kubectl get secret tap-values -n tap-install -o jsonpath="{.data['tap-values\.yaml']}" | base64 -d
```

```bash
tanzu apps workload create tanzu-java-web-app \
   --git-repo https://github.com/poprygun/tanzu-java-web-app.git \
   --git-branch master \
   --type web \
   --label app.kubernetes.io/part-of=tanzu-java-web-app \
   --label apps.tanzu.vmware.com/has-tests=true \
   --yes \
   --namespace my-apps
```

## View build logs

```bash
kp build logs tanzu-java-web-app
```

## Show Image volnurabilities

```bash
kubectl get imagescan
```

## Tail application logs

```bash
tanzu apps workload tail tanzu-java-web-app --since 10m --timestamp -n my-apps
```

## Determine Cluster Name

```bash
kubectl config view --minify
```

## References

[Deploy a Test Workload to a Workload or Unmanaged Cluster](https://tanzucommunityedition.io/docs/v0.12/sample/#deploy-a-test-workload-to-a-workload-or-unmanaged-cluster)

[Tanzu Cluster Commands](https://tanzucommunityedition.io/docs/v0.12/ref-unmanaged-cluster/)




