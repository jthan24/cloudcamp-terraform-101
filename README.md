# cloudcamp-terraform-101


## instalacion

### agregar el terraform a nuestra distribucion
```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform
```

```bash
terraform -version
```

### auto completar (optional)
```bash
terraform -install-autocomplete
```


## uso de un provider
```bash

cd ~ && mkdir primera_chamba_docker && cd primera_chamba_docker 


tee -a main.tf <<EOF

terraform {
  required_providers {
	docker = {
  	source  = "kreuzwerker/docker"
  	version = "~> 3.0.1"
	}
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"

  ports {
    internal = 80
    external = 8000
  }
}

EOF
```


## inicializar el codigo
```bash
terraform init
```

## formatear el codigo
```bash
cat main.tf
terraform fmt
cat main.tf
```

## desplegar la infraestructura
```bash
terraform apply
```


## resources
https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli