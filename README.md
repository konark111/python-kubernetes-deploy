# python-kubernetes-deployment
# Tools used
- Docker
- Kubernetes

We use config maps and secrets to store values so that it can be used by pod at later point of time for e.g. db-port, db connection type, username, password.
Key difference bw config maps and secrets is that we use config maps to mostly store non-sensitive data and secrets for sensitive data. As all data for config-maps is stored in etcd as objects any malicious user can retrieve the sensitive data and compromise the application but with secrets it is encrypted before saving it to etcd so without decrytion key that data is useless.

There are 2 methods of using config map values in pod i.e via volume mount and env var.
  EnvVar - We can call values in pod with env vars but issue is that if these values change in future, we would have to recreate pods as we cannot  
  change the env vars in running container and it can lead to traffic loss or data loss.
  Volumes - Resolves the values changing from time to time problem as it shall update the pods with new values from config maps without restarting 
  the pod.

# More security can be implemented via implementation of strict RBAC policies 
  - Least privilege : RBAC policy defined in a way that no normal user shall have access to secrets.
  - Use Secret manager : As k8s encryption is not great we can look for other solutions as hashicorp vault.
