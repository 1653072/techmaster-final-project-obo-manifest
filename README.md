### OBO K8S MANIFEST

1. **Manual Commands**:
    - Start application and database:
        - $ kubectl apply -f ./templates/obo_config.yaml && kubectl apply -f ./templates/mysql_init_file.yaml && kubectl
          apply -f ./templates/mysql_config.yaml && kubectl apply -f ./templates/db_deployment.yaml
        - $ kubectl get pods -o wide (Before executing next commands, please wait at least 20 seconds to help MySQL
          finish initializing the _obo_ database and its respective tables).
        - $ kubectl apply -f ./templates/app_deployment.yaml (We should run this app_deployment after MySQL in
          db_deployment is running more than 20 seconds)
        - $ kubectl get nodes,services,deployments,secrets,configmaps,pods -o wide
    - Cleanup everything:
        - $ kubectl delete -f ./templates

2. **Notes**:
    - The app service will be exported in the NodePort **30000**.
    - To access the MySQL pod to execute any DDL or DML queries:
        - $ kubectl exec -it <mysql_pod_name> -- sh
        - $ ls -l /docker-entrypoint-initdb.d (To view the file used to initialize MySQL database).
        - $ ls -l /var/lib/mysql (To view the generated database folder).
        - $ mysql -u root -h localhost -p (To access MySQL with the root user and the given _"mysql"_ password which was
          provided in the MYSQL_ROOT_PASSWORD config key).
        - $ use obo; (Use "obo" database name).
        - $ show tables; (Show all tables in the given database).
        - $ select * from users; (To view a list of users in the "users" table).
        - $ exit (Exit the current MySQL session).
        - $ exit (Exit the current pod session).

3. **References**:
    - Obo Github: https://github.com/orez-fu/obo/tree/main
