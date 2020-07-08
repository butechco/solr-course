(cd configset/produto && zip -r - *) > produtoconfigset.zip

Para fazer upload
curl -X POST --header "Content-Type:application/octet-stream" --data-binary @produtoconfigset.zip "http://localhost:8983/solr/admin/configs?action=UPLOAD&name=produtoConfigSet"

Para ver se o configset subiu
curl "http://localhost:8983/api/cluster/configs?omitHeader=true"

Para apagar
curl "http://localhost:8983/solr/admin/configs?action=DELETE&name=produtoConfigSet&omitHeader=true"

CRIAR COLECAO
curl "http://localhost:8983/solr/admin/collections?action=CREATE&name=produto&numShards=1&collection.configName=produtoConfigSet&wt=json"

APAGAR COLECAO
curl "http://localhost:8983/solr/admin/collections?action=DELETE&name=produto&wt=xml"

INDEXAR DOCUMENTOS
curl -X POST -H 'Content-Type: application/json' 'http://localhost:8983/solr/produto/update?commit=true' --data-binary '[
{
    "id":1614132251,
    "titulo":"iPhone 11 64GB Branco iOS 4G Câmera 12MP",
    "marca":"Apple",
    "loja":"Fast Shop",
    "preco":4820.58,
    "url":"https://www.submarino.com.br/produto/1614132251/iphone-11-64gb-branco-ios-4g-camera-12mp-apple",
    "imagem":"https://images-submarino.b2w.io/produtos/01/00/img/1614132/3/1614132374_1GG.jpg",
    "avaliacao":4,
    "parcelas":12,
    "sem_juros":true
},
{
    "id":462138611,
    "titulo":"Smartphone Motorola Moto G8 Plus 64GB Dual Chip Android 6.3\" Qualcomm Snapdragon 665 (SM6125) 4G Câmera 48MP + 5MP + 16MP- Azul Safira",
    "marca":"Motorola",
    "loja":"Submariono",
    "preco":1499.00,
    "url":"https://www.submarino.com.br/produto/462138611/smartphone-motorola-moto-g8-plus-64gb-dual-chip-android-6-3-qualcomm-snapdragon-665-sm6125-4g-camera-48mp-5mp-16mp-azul-safira?pfm_carac=celular%20motorola&pfm_index=1&pfm_page=search&pfm_pos=grid&pfm_type=search_page",
    "imagem":"https://images-submarino.b2w.io/produtos/01/00/img7/01/00/item/462138/6/462138611_1GG.jpg",
    "avaliacao":4,
    "parcelas":12,
    "sem_juros":true
},
{
    "id":360560511,
    "titulo":"Smartphone Samsung Galaxy A30s 64GB Dual Chip Android 9.0 Tela 6.4\" Octa-Core 4G Câmera Tripla 25MP + 5MP + 8MP - Preto",
    "marca":"Samsung",
    "loja":"Submarino",
    "preco":1399.00,
    "url":"https://www.submarino.com.br/produto/360560511/smartphone-samsung-galaxy-a30s-64gb-dual-chip-android-9-0-tela-6-4-octa-core-4g-camera-tripla-25mp-5mp-8mp-preto?pfm_carac=celular%20galaxy&pfm_page=search&pfm_pos=grid&pfm_type=search_page",
    "imagem":"https://images-submarino.b2w.io/produtos/01/00/img/360560/5/360560538_1GG.jpg",
    "avaliacao":4,
    "parcelas":12,
    "sem_juros":true
}]'

APAGAR DOCUMENTOS
<delete><query>*:*</query></delete>

CRIAR NOVO CAMPO
curl -X POST -H 'Content-type:application/json' --data-binary '{
    "add-field": {
        "name": "click_count",
        "type": "pint",
        "indexed": true,
        "stored": true,
        "required": false
    }
}' http://localhost:8983/api/collections/produto/schema


curl "http://localhost:8983/solr/admin/collections?action=CREATE&name=materiais&numShards=1&collection.configName=produtoConfigSet&wt=json"
