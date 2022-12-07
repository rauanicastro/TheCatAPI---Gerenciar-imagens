## Gerenciar imagens

Aprenda a gerenciar as imagens de gatos dentro do sistema da The Cat API.

### Visão geral

Com o recurso Images é possível criar, obter e excluir imagens de gatos no nosso sistema. 

Para realizar as chamadas, é obrigatório ter uma API Key. Para obtê-la, registre-se em https://thecatapi.com/signup e receba a API Key por e-mail. A sua API Key deve ser informada no header, na variável `x-api-key`. O `path` utilizado nas chamadas é https://api.thecatapi.com/v1.

---

###  Criar imagem


Para criar uma nova imagem de gato no sistema, chame `POST /images/upload` e preencha o corpo da requisição com um `file` contendo o arquivo. Imagens que sejam inapropriadas ou que não contiverem gatos serão recusadas, e é obrigatório que o arquivo de imagem seja .gif, .jpg, ou .png válido.

>Observação: se já houver um `id` da imagem para identificação interna, preencha o corpo da requisição com `sub_id` do tipo `string`.
 
    curl --location --request POST 'https://api.thecatapi.com/v1/images/upload' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB' \
    --form 'file=@"81Oj_pa-N/gato-preto-1666974144631_v2_3x4.jpg"'

A resposta do código  `201 Created` indica que a criação da imagem foi executada com sucesso, e retorna um JSON com as informações da imagem, incluindo seu novo `id` . O `id` é gerado automaticamente pelo sistema. Por exemplo:


       {
        "id": "6Y8Bdvw1A",
        "url": "https://cdn2.thecatapi.com/images/6Y8Bdvw1A.jpg",
        "width": 1059,
        "height": 1413,
        "original_filename": "gato-preto-1666974144631_v2_3x4.jpg",
        "pending": 0,
        "approved": 1
    }


### Obter imagem

Há mais de uma forma para obter as imagens que foram enviadas através do `/images/upload`. São elas:
 1. Get by ID
 2. GET

#### 1. GET by ID

Para obter uma imagem específica, chame `GET /images/{image_id}` como `path`. O parâmetro `image_id` deve ser composto apenas do `id` da imagem que você deseja obter. Por exemplo:

    curl --location --request GET 'https://api.thecatapi.com/v1/images/6Y8Bdvw1A' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB'

A resposta do código `200 OK` indica que a imagem foi obtida com sucesso, e retorna um JSON com as informações da imagem encontrada. Por exemplo:

    "id":  "6Y8Bdvw1A",
    
    "url":  "https://cdn2.thecatapi.com/images/6Y8Bdvw1A.jpg",
    
    "width":  1059,
    
    "height":  1413,
    
    "sub_id":  null
    
    }



#### 2. GET

Outra opção para obter as imagens é chamar `GET /images` como `path` para poder filtrar os resultados através dos seguintes parâmetros `query`:

 - `limit`

O parâmetro `limit` é do tipo `integer` e funciona para delimitar o número de resultados a serem retornados. O padrão do parâmetro `limit` é 1, portanto, para obter mais imagens, insira o valor desejado. Por exemplo:

    curl --location --request GET 'https://api.thecatapi.com/v1/images?limit=2' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB'

A resposta do código `200 OK` indica que as imagens foram obtidas com sucesso, e retorna um JSON com as informações das imagens encontradas. Por exemplo:

    [
        {
            "breeds": [],
            "id": "6Y8Bdvw1A",
            "url": "https://cdn2.thecatapi.com/images/6Y8Bdvw1A.jpg",
            "width": 1059,
            "height": 1413,
            "sub_id": null,
            "created_at": "2022-12-01T00:13:48.000Z",
            "original_filename": "gato-preto-1666974144631_v2_3x4.jpg",
            "breed_ids": null
        },
        {
            "breeds": [],
            "id": "gsa7n-0Ek",
            "url": "https://cdn2.thecatapi.com/images/gsa7n-0Ek.jpg",
            "width": 700,
            "height": 466,
            "sub_id": null,
            "created_at": "2022-12-01T00:11:13.000Z",
            "original_filename": "25516126.jpg",
            "breed_ids": null
        }
    ]

 - `mime_types`

Esse parâmetro é do tipo `string` delimitado por vírgulas e filtra as imagens como  **.gif**, **.jpg**, ou **.png**. O `mime_types` retorna todos esses três tipos de imagem como padrão. Abaixo, um exemplo de chamada para obter três imagens filtradas por .png e .jpg:

     curl --location --request GET 'https://api.thecatapi.com/v1/images?limit=3&order=png,jpg' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB'

A resposta do código `200 OK` indica que as imagens foram obtidas com sucesso, e retorna um JSON com as informações das imagens encontradas. Por exemplo:

        [
        {
            "breeds": [],
            "id": "bezC2JyB3",
            "url": "https://cdn2.thecatapi.com/images/bezC2JyB3.jpg",
            "width": 700,
            "height": 466,
            "sub_id": null,
            "created_at": "2022-12-01T00:09:38.000Z",
            "original_filename": "25516126.jpg",
            "breed_ids": null
        },
        {
            "breeds": [],
            "id": "S1NMmWujv",
            "url": "https://cdn2.thecatapi.com/images/S1NMmWujv.jpg",
            "width": 360,
            "height": 360,
            "sub_id": null,
            "created_at": "2022-12-01T15:12:54.000Z",
            "original_filename": "cat_01.jpg",
            "breed_ids": null
        },
        {
            "breeds": [],
            "id": "vEPpiDG_p",
            "url": "https://cdn2.thecatapi.com/images/vEPpiDG_p.png",
            "width": 360,
            "height": 636,
            "sub_id": null,
            "created_at": "2022-12-02T13:07:30.000Z",
            "original_filename": "png-transparent-himalayan-cat-thai-cat-siamese-cat-balinese-cat-birman-ragdoll-cat-mammal-animals-ca",
            "breed_ids": null
        }
    ]

 - `order`

O parâmetro `order` é do tipo `string` e permite que as imagens sejam obtidas de forma ordenada usando **RANDOM**, **ASC** ou **DESC**. O padrão é **RANDOM**. Por exemplo:

    curl --location --request GET 'https://api.thecatapi.com/v1/images?limit=2&order' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB'

A resposta do código `200 OK` indica que as imagens foram obtidas com sucesso em ordem aleatória, e retorna um JSON com as informações das imagens encontradas. Por exemplo:

    [
        {
            "breeds": [],
            "id": "x94CCTLLe",
            "url": "https://cdn2.thecatapi.com/images/x94CCTLLe.jpg",
            "width": 360,
            "height": 360,
            "sub_id": null,
            "created_at": "2022-12-01T00:28:09.000Z",
            "original_filename": "cat_01.jpg",
            "breed_ids": null
        },
        {
            "breeds": [],
            "id": "gsa7n-0Ek",
            "url": "https://cdn2.thecatapi.com/images/gsa7n-0Ek.jpg",
            "width": 700,
            "height": 466,
            "sub_id": null,
            "created_at": "2022-12-01T00:11:13.000Z",
            "original_filename": "25516126.jpg",
            "breed_ids": null
        }
    ]


Para filtrar as imagens em ordem ascendente de tamanho, use **ASC** no parâmetro `order`. Por exemplo:

    curl --location --request GET 'https://api.thecatapi.com/v1/images?limit=2&order=ASC' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB'

A resposta do código `200 OK` indica que as imagens foram obtidas com sucesso em ordem ascendente, e retorna um JSON com as informações das imagens encontradas. Por exemplo:

    [
        {
            "breeds": [],
            "id": "V1EFdLiCO",
            "url": "https://cdn2.thecatapi.com/images/V1EFdLiCO.png",
            "width": 860,
            "height": 733,
            "sub_id": null,
            "created_at": "2022-11-24T15:28:59.000Z",
            "original_filename": "41-415477_cat-tongue-png-cute-cat-png-transparent-png.png",
            "breed_ids": null
        },
        {
            "breeds": [],
            "id": "uDA8Z17di",
            "url": "https://cdn2.thecatapi.com/images/uDA8Z17di.jpg",
            "width": 275,
            "height": 183,
            "sub_id": null,
            "created_at": "2022-11-24T16:35:58.000Z",
            "original_filename": "index.jpg",
            "breed_ids": null
        }
    ]


Para filtrar as imagens em ordem descendente de tamanho, use **DESC** no parâmetro `order`. Por exemplo:

      curl --location --request GET 'https://api.thecatapi.com/v1/images?limit=2&order=DESC' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB'

A resposta do código `200 OK` indica que as imagens foram obtidas com sucesso em ordem descendente, e retorna um JSON com as informações das imagens encontradas. Por exemplo:

       [
        {
            "breeds": [],
            "id": "x94CCTLLe",
            "url": "https://cdn2.thecatapi.com/images/x94CCTLLe.jpg",
            "width": 360,
            "height": 360,
            "sub_id": null,
            "created_at": "2022-12-01T00:28:09.000Z",
            "original_filename": "cat_01.jpg",
            "breed_ids": null
        },
        {
            "breeds": [],
            "id": "gsa7n-0Ek",
            "url": "https://cdn2.thecatapi.com/images/gsa7n-0Ek.jpg",
            "width": 700,
            "height": 466,
            "sub_id": null,
            "created_at": "2022-12-01T00:11:13.000Z",
            "original_filename": "25516126.jpg",
            "breed_ids": null
        }
    ]


### Deletar imagem

Para excluir uma imagem, chame `DELETE /images/{image_id}` passado como parâmetro `path`. O parâmetro `image_id` deve ser composto apenas do `id` da imagem que você deseja excluir. Por exemplo:

    curl --location --request DELETE 'https://api.thecatapi.com/v1/images/6Y8Bdvw1A' \
    --header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB'

A resposta de código `204 No Content` indica que a imagem foi excluída com sucesso e o sistema não retorna um JSON nesse caso.


