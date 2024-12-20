# Validação de Cache na Akamai

## **1. Introdução**
Este documento detalha os procedimentos para validar se uma API está sendo servida pelo cache da Akamai. Inclui passos para verificação em tempo real, análise de relatórios e validação de configurações no painel Akamai Control Center.

---

## **2. Validação via Linha de Comando**

### **Requisições Consecutivas com `curl`**
Execute duas ou mais requisições HTTP para a API e capture os cabeçalhos.

**Comando:**
```bash
# Primeira requisição (possível MISS)
curl -I -H "Pragma: akamai-x-cache-on, akamai-x-get-cache-key" https://api.seudominio.com/endpoint > primeira_resposta.txt

# Segunda requisição (possível HIT)
curl -I -H "Pragma: akamai-x-cache-on, akamai-x-get-cache-key" https://api.seudominio.com/endpoint > segunda_resposta.txt
```

**Cabeçalhos relevantes:**
- `X-Cache`: Indica o status do cache.
  - **`TCP_HIT`**: Conteúdo entregue pelo cache.
  - **`TCP_MISS`**: Conteúdo buscado na origem.
- `X-Cache-Key`: Chave do objeto no cache.
- `Age`: Tempo de vida do conteúdo no cache.
- `Cache-Control` ou `Expires`: Políticas de cache.

**Exemplo de resposta:**
```plaintext
HTTP/1.1 200 OK
X-Cache: TCP_HIT from a12345.akamai.net (L1)
X-Cache-Key: /L/1234/your-endpoint
Age: 120
Cache-Control: max-age=300
```

---

## **3. Validação no Painel Akamai Control Center**

### **Acessar o Painel**
1. Entre no [**Akamai Control Center**](https://control.akamai.com).
2. Faça login com suas credenciais.

### **Ferramenta Content Delivery Reports**
1. Navegue para **`Monitor > Content Delivery Reports`**.
2. Selecione a **Property** associada à API.
3. Configure os filtros:
   - Período de tempo (ex: últimas 24 horas).
   - Tipo de entrega: **Cache Hit/Miss**.
4. Gere o relatório e verifique:
   - **Cache Hit Ratio**: Gráfico com a proporção de HITs/MISSes.

---

### **Ferramenta Edge Diagnostics**
1. Acesse **`Support > Edge Diagnostics`** no painel.
2. Utilize **`EdgeScape > Diagnostic Tools`**.
3. Escolha a opção **"URL Testing"**.
   - Insira a URL da API.
   - Clique em **"Run Test"**.

**Resultados esperados:**
- **X-Cache**: Exibe HIT ou MISS.
- **X-Cache-Key**: Chave utilizada no cache.
- **Age**: Tempo que o objeto está no cache.

---

### **Ferramenta Property Manager**
1. Acesse **`Configure > Property Manager`**.
2. Localize a **Property** associada à API.
3. Revise as regras de cache:
   - **Caching Rules**:
     - `Time To Live (TTL)` definido.
   - **Bypass Cache Rules** (se existirem).

**Visualização:** Utilize a opção **"Rule Tree View"** para uma visão detalhada.

---

## **4. Relatório Consolidado de Validação**
Para documentar a evidência:
1. **Capture os logs das requisições**:
   - Primeira requisição (**MISS**): `primeira_resposta.txt`
   - Segunda requisição (**HIT**): `segunda_resposta.txt`
2. **Gráficos e relatórios**:
   - Exportar relatórios de **Cache Hit/Miss** do painel Akamai.
3. **Capturas de tela**:
   - Tela da ferramenta **Edge Diagnostics** com os cabeçalhos relevantes.
   - Visualização do Property Manager com regras de cache.

**Exemplo de Evidência:**
```plaintext
HTTP/1.1 200 OK
X-Cache: TCP_HIT from a12345.akamai.net (L1)
X-Cache-Key: /L/1234/your-endpoint
Age: 120
Cache-Control: max-age=300
```

**Comparativo de Tempo de Resposta:**
- Primeira requisição (MISS): **0.250s**
- Segunda requisição (HIT): **0.050s**

---

## **5. Conclusão**
Utilizando as ferramentas acima, é possível validar e documentar a presença do cache na Akamai para uma API. O uso de cabeçalhos como **X-Cache**, **Age**, e relatórios no painel fornece evidências claras do comportamento do cache.

---

## **Referências**
- [Akamai Control Center](https://control.akamai.com)
- [Documentação Akamai Edge Diagnostics](https://techdocs.akamai.com/edge-diagnostics/)
