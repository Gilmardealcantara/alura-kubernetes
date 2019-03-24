# Alura-kubernetes
Kubernetes Alura Course

###  Deploy 
* Install minikube and virtual box version 5.2
#### Database
```shellscript
$ minikub start
$ cd kubernetes/db/
$ kubectl create -f statefulset.yaml
$ kubectl create -f database-service.yaml
$ kubectl create -f permissions.yaml
$ kubectl get pods
$ kubectl exec -it [mysql pod name]  sh
# mysql -u root
mysql> user loja
```
Paste the mysql script:
```mysql
create table produtos (id integer auto_increment primary key, nome varchar(255), preco decimal(10,2));
alter table produtos add column usado boolean default false;
alter table produtos add column descricao varchar(255);
create table categorias (id integer auto_increment primary key, nome varchar(255));
insert into categorias (nome) values ("Futebol"), ("Volei"), ("Tenis");
alter table produtos add column categoria_id integer;
update produtos set categoria_id = 1;
```

#### APP
```shellscript
$ cd kubernetes/app/
$ kubectl create -f deployment.yaml
$ kubectl create -f app-service.yaml
$ kubectl scale deployment app-deployment --replicas=3
$ kubectl get pods
$ minikube service app-service --url
```
