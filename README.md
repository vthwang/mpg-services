# mpgServices
1. `helm install mpg-services . --create-namespace -n mpg-services`.
2. Create secret.
   ```
   kubectl \
   create secret generic mpg-mongo-secret \
   -n mpg-services \
   --from-literal="MONGO_INITDB_ROOT_USERNAME=admin" \
   --from-literal="MONGO_INITDB_ROOT_PASSWORD=password"
   ```
3. `kubectl apply -f pvc.yaml`