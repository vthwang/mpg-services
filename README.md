# mpgServices
## Install services
1. Create Secret.
   ```
   kubectl \
   create secret generic mpg-mongo-secret \
   -n mpg-services \
   --from-literal="MONGO_INITDB_ROOT_USERNAME=admin" \
   --from-literal="MONGO_INITDB_ROOT_PASSWORD=password"
   ```
2. Create Volume.
   `kubectl apply -f pvc.yaml`
3. Install helm services.
   `helm install mpg-services . --create-namespace -n mpg-services`.
4. Upgrade
   `helm upgrade mpg-services . -n mpg-services`

## Generate ssl
1. `openssl genrsa -out root-ca.key 2048`
2. ```
   openssl req -x509 -new -nodes -key root-ca.key -sha256 \
   -days 1024 -out root-ca.pem
   ```
3. `openssl genrsa -out mongodb.key 2048`
4. `openssl req -new -key mongodb.key -out mongodb.csr`
5. ```
   openssl x509 -req -in mongodb.csr -CA root-ca.pem \
   -CAkey root-ca.key -CAcreateserial -out mongodb.crt \
   -days 700 -sha256
   ```
   
## Reference
1. [Mongo SSL Auth on Kubernetes](https://vladroff.medium.com/mongodb-ssl-auth-on-kubernetes-ee14bf1a744f)