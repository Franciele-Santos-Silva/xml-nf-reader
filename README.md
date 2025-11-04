# Leitor de XML de Notas Fiscais

Este projeto tem como objetivo **ler arquivos XML de Notas Fiscais eletrônicas (NF-e)**, extrair informações relevantes e **gerar uma planilha Excel (`Notas_Fiscais.xlsx`)** contendo os principais dados das notas.

## Funcionalidades

- Leitura automática de todos os arquivos `.xml` localizados na pasta `nfs/`;
- Extração de informações essenciais de cada nota fiscal:
  - Número da nota (`Id`);
  - Nome da empresa emissora;
  - Nome do cliente;
  - Endereço do destinatário;
  - Peso bruto (`pesoB`);
- Exportação dos dados para um arquivo Excel de forma organizada.

## Tecnologias Utilizadas

- **Python 3.10+**
- **Bibliotecas:**
  - [`xmltodict`](https://pypi.org/project/xmltodict/) → para converter o XML em dicionário Python;
  - [`os`](https://docs.python.org/3/library/os.html) → para percorrer os arquivos da pasta;
  - [`pandas`](https://pandas.pydata.org/) → para criar e exportar os dados em formato Excel.
  - [`openpyxl`](https://openpyxl.readthedocs.io/) → engine utilizada pelo pandas para escrever arquivos Excel (`.xlsx`).

## Como Executar o Projeto

1. Clone o repositório ou baixe o projeto:

        git clone https://github.com/FRANCIELE-SANTOS-SILVA/xml-nf-reader.git
        cd xml-nf-reader

2. Crie e ative o ambiente virtual:

        python -m venv venv
        venv\Scripts\activate     

3. Instale as dependências:

        pip install xmltodict pandas openpyxl

4. Adicione seus arquivos `.xml` na pasta `nfs/`.

5. Execute o script:

        python main.py

6. Verifique o resultado:

   Um arquivo chamado **`Notas_Fiscais.xlsx`** será gerado na raiz do projeto contendo as informações extraídas.

## Exemplo de Saída (Excel)

| numero_nota                             | empresa_emissora                        | nome_cliente        | endereco (dicionário)                                                                                             | peso  |
|----------------------------------------|-----------------------------------------|---------------------|-------------------------------------------------------------------------------------------------------------------|-------|
| NFe35080599999090910270550010000000015180051273 | NF-e Associacao NF-e                    | DISTRIBUIDORA DE AGUAS MINERAIS | {'xLgr': 'AV DAS FONTES', 'nro': '1777', 'xCpl': '10 ANDAR', 'xBairro': 'PARQUE FONTES', ...}                    | 1200000000.000 |
| NFe33211160409075055054550050001739511658504115 | NESTLE BRASIL LTDA                      | Lira da Hashtag     | {'xLgr': 'Rua Nem vem que nao tem', 'nro': '12', 'xBairro': 'semapt', 'xMun': 'Rio de Janeiro', 'UF': 'RJ', ...} | 0     |
| NFe35211136882195000279550010000028500052336     | BROTA COMPANY COMERCIO DE PLANTAS LTDA | Lira da Hashtag     | {'xLgr': 'Perdido no Espaco', 'nro': '0', 'xBairro': 'Lua', 'xMun': 'Rio de Janeiro', 'UF': 'RJ', ...}           | 2.600 |

## Observações

- Caso alguma nota fiscal **não contenha o campo `<vol>`**, o peso será automaticamente definido como `"0"`.
- O código trata tanto XMLs com a tag raiz `<NFe>` quanto com `<nfeProc>`, garantindo compatibilidade com diferentes formatos de exportação de NF-e.
