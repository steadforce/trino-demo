# Trino Demo

Repository containing manifests for installing a demo which showcases how to use trino to execute queries from multiple sources. Never install the content of this repo on our clusters manually. This is all done by argo-cd.

## Dependencies

This chart has no dependencies specified in `Chart.yaml`. However, in order for it to work you have to have a running trino server by e.g. using [this trino deployment](https://github.com/steadforce/trino).

## Render helm charts locally

The following command renders the charts like argo-cd does to validate the content.

```
 helm template --release-name trino-demo -n trino-demo --skip-tests \
  --output-dir _render/ . 
```

You can use this command to check if the output is as you expect. The `-a` parameters are needed since we use the
helm feature `.Capabilities.APIVersions.Has` to determine if a `CR` is installable in the cluster or not. Since
helm templating is designed to work offline we have to list the supported `CR`. Using `.Capabilities.APIVersions.Has`
feature in templating prevents sync errors in argo-cd if a `CR` can't be applied since its `CRD` isn't ready.