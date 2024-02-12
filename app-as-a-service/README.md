# App as a Service

> **Warning**
>
> **To use this Promise, the Kubernetes cluster running Kratix must be registered
as a Destination with the label `environment=platform`**
>
> Check out the [Compound Promises
guide](https://kratix.io/docs/main/guides/compound-promises) on the Kratix
documentation for details on how to setup your platform.

This Promise provides Compound App-as-a-Service promise with two `requiredPromises`. This is a compound Promise that installs the following Promises:

- [Nginx-ingress](https://github.com/syntasso/kratix-marketplace/tree/main/nginx-ingress)
- [Postgres](https://github.com/syntasso/kratix-marketplace/tree/main/postgresql)
- [Deployment](../deployment/) (which deploys the sample application to the Destination with the configured ingress)

The following fields are configurable:

- name: application name
- image: application image
- dbDriver: db type, only postgresql or none are valid options currently

To install:
```
kubectl create -f https://raw.githubusercontent.com/syntasso/kratix/main/samples/paved-path-nginx/promise.yaml
```

To make a resource request:
```
kubectl apply -f https://raw.githubusercontent.com/syntasso/kratix/main/samples/paved-path-nginx/resource-request.yaml
```

This resource request deploys the Kratix [sample Golang app](https://github.com/syntasso/sample-golang-app).

To test the sample app once it is successfully deployed, port forward with command
below and access at `http://localhost:8080`, ensure you have the
`Host: todo.example.com` set in your browser:
```
kubectl --context kind-worker port-forward svc/nginx-nginx-ingress 8080:80
```

## Development

For development see [README.md](./internal/README.md)

## Questions? Feedback?

We are always looking for ways to improve Kratix and the [Marketplace](kratix.io/marketplace). If you run into issues or have ideas for us, please let us know. Feel free to [open an issue](https://github.com/syntasso/kratix-marketplace/issues/new/choose) or [put time on our calendar](https://www.syntasso.io/contact-us). We'd love to hear from you.
