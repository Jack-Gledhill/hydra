# Cloud Native PostgreSQL Operator (CNPG)

**Note:** you'll need to do a server-side apply on this kustomisation. 
This is because CNPG has an annotation that exceeds the normal size limit, which causes a normal `kubectl apply` to fail unless `--server-side-apply` is specified.