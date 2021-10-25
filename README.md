This repo doesn't work.

If you have a chart that includes logzio-otel-traces as a subchart, the installation fails.

```
minikube start --kubernetes-version=v1.20.5
```


Install this repo, with logzio-otel-traces installed as a subchart.

```
helm dep build .
helm install logzio-otel-traces-test . --set logzio-otel-traces.config.exporters.logzio.account_token=XXXX
```


and this is what we get

```
→ kubectl get pods
NAME                                       READY   STATUS             RESTARTS   AGE
logzio-otel-traces-test-64c9d56f99-5r4vx   0/1     CrashLoopBackOff   6          6m32s
```

```
kubectl logs logzio-otel-traces-test-64c9d56f99-5r4vx
2021-10-25T21:07:43.445Z	info	service/collector.go:303	Starting otelcontribcol...	{"Version": "v0.35.0", "NumCPU": 32}
2021-10-25T21:07:43.445Z	warn	service/collector.go:312	`mem-ballast-size-mib` command line option has been deprecated. Please use `ballast extension` instead!
2021-10-25T21:07:43.445Z	info	service/collector.go:242	Loading configuration...
Error: invalid configuration: service references extension "health_check" which does not exist
2021/10/25 21:07:43 collector server run finished with error: invalid configuration: service references extension "health_check" which does not exist
```
