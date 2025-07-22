# Zabbix Export Items
Script Python para exportar itens monitorados de hosts no Zabbix, organizado por grupos, e gerar um relatório em Excel.

## 🧩 Descrição
O `export-items.py` conecta-se ao Zabbix via API, obtém itens de hosts em um ou mais grupos e exporta os dados para uma planilha `.xlsx`, com cada grupo em uma aba separada.

## ⚙️ Requisitos
- Python 3.7+
- Módulos Python:

```nginx
pip install pyzabbix openpyxl argparse tqdm
```
(Adicione quaisquer outros módulos especificados no script, como pyfiglet por ex.)

## 🚀 Uso
```bash
python export-items.py -s <URL_ZABBIX> -u <USUARIO> -p <SENHA> [-g <ID_GRUPO>...] [-n <NOME_RELATORIO>]
```

### Parâmetros principais
- -s, --server: URL do Zabbix (ex: http://localhost/zabbix)
- -u, --user: usuário da API (ex: Admin)
- -p, --password: senha do usuário
- -g, --group: IDs de grupos de host (opcional). Pode repetir para múltiplos grupos.
- -n, --name: nome base para o relatório (ex: CLIENT). Será salvo como CLIENT_<DATA>.xlsx.

### Exemplos
- Exportar todos os grupos:

```bash
python export-items.py -s http://zabbix.local -u Admin -p secret
```
- Exportar grupos específicos:

```bash
python export-items.py -s http://zabbix.local -u Admin -p secret -g 1 -g 2 -n CLIENT
```
- Exibir ajuda:

```bash
python export-items.py -h
```
## 📄 Saída
Um arquivo `.xlsx` será gerado no diretório atual, nomeado como `<NOME>_<YYYYMMDD>.xlsx`.

Cada grupo de hosts terá uma aba com linhas representando os itens (nome, tipo, host, chave, valor, etc.).

## 🛠️ Implementação (resumo)
- Conexão com API do Zabbix usando pyzabbix.
- Leitura dos parâmetros de linha de comando via argparse.
- Consulta para listar grupos (group.get) e hosts (host.get) por grupo.
- Extração de itens por host (item.get).
- Escrita no Excel com múltiplas abas usando openpyxl.
- Barra de progresso exibida com tqdm.
