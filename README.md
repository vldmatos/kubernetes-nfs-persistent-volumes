# Persistent Volumes NFS Kubernetes

## Server NFS

Instalação do serviço de NFS no servidor NFS  
Neste exemplo utilizando um node do cluster kubernetes  
Instalando serviço  

```bash
sudo apt-get install nfs-kernel-server  
```

Criando diretorio NFS  
```bash
sudo mkdir /srv/nfs
```

Permissão para usuário pod se necessário  
```bash
sudo chown -R 1000 /srv/nfs
```

Criando arquivo de configuração para NFS    
```bash
sudo vim /etc/exports
```

Conteudo do arquivo.  
```
/srv/nfs    *(rw,sync,no_subtree_check,no_root_squash,no_all_squash,insecure)
```

Inicializando o serviço, configuração e verificando o compartilhamento 
```bash
sudo systemctl enable --now nfs-server
sudo exportfs -rav
showmount -e localhost
```


## Clients NFS
Instalando serviço nos clients NFS, todos os nos que do pods que vão utilizar os pvs  
```bash
sudo apt-get update
sudo apt-get install nfs-common
```

## Criar recursos do kubernetes
Arquivos disponíveis no repositório.

- Persistent Volume
- Persistent Volume Claim
- Deployment