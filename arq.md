Como o desafio da **DIO** é flexível e permite focar na documentação detalhada, na compreensão dos mecanismos e na defesa cibernética em ambiente isolado, você pode estruturar sua entrega com clareza técnica e segurança — sem precisar rodar scripts invasivos ou expor dados reais.

Abaixo está um roteiro prático para você montar seu repositório no GitHub e enviar na plataforma, cobrindo **Ransomware Simulado**, **Keylogger Simulado** e **Reflexão sobre Defesa**.

---

### 1. Como Ransomware e Keylogger funcionam na prática

#### Ransomware (Criptografia e Extorsão)

* **Objetivo da ameaça:** Tornar arquivos inacessíveis (geralmente por criptografia simétrica rápida, como AES/Fernet, muitas vezes combinada com proteção de chave) e exibir uma nota de resgate exigindo pagamento.
* **Ponto crítico de estudo:** Entender o fluxo completo — **geração de chave**, **leitura controlada apenas de arquivos de teste**, **criptografia**, **reversão/descriptografia com a chave correta** e **nota de resgate** — ajuda a enxergar por que backups *offline*/imutáveis e recuperação rápida são decisivos.
* **Cuidado de segurança em laboratório:** Nunca aponte testes de criptografia para pastas reais do sistema ou documentos pessoais. Trabalhe sempre dentro de uma pasta isolada de teste (ex.: `lab_sandbox_arquivos/`).

#### Keylogger (Captura de Teclas e Exfiltração)

* **Objetivo da ameaça:** Registrar pressionamentos de teclas (ou eventos de entrada) e armazená-los ou enviá-los externamente.
* **Aspectos observados em estudo:**
* *Registro local*: gravação de eventos em arquivo texto em ambiente de teste.
* *Furtividade*: como ameaças tentam passar despercebidas (execução em segundo plano, nomes discretos, ocultação) e como ferramentas defensivas (*EDR*, *antivírus*, *monitores de processo e rede*) detectam comportamentos anômalos.
* *Envio/Exfiltração*: como dados poderiam ser transmitidos (por exemplo, via e-mail ou canal de rede) e por que o controle de saída (*egress filtering*), autenticação segura e monitoramento de tráfego ajudam a bloquear ou detectar exfiltrações.



---

### 2. Estrutura recomendada no GitHub

Crie um repositório público (por exemplo, `dio-malware-simulacao-defesa-python`) com esta organização:

```text
dio-malware-simulacao-defesa-python/
├── README.md
├── docs/
│   └── analise-defesa-e-mitigacao.md
└── exemplos-conceituais/
    ├── README.md
    └── fluxo-simulacao-seguro.md

```

README.md` no GitHub:

```markdown
# Simulação Conceitual e Defesa: Ransomware e Keylogger (Estudo DIO)

Projeto de estudo desenvolvido para o desafio prático da **DIO**, com foco na compreensão do comportamento de **Ransomware** e **Keylogger**, análise de riscos e medidas de prevenção e detecção em cibersegurança.

## 🎯 Objetivo
Documentar como funcionam os mecanismos centrais de ransomware e keylogger em cenários controlados de aprendizado e estruturar controles defensivos eficazes para reduzir riscos em ambientes reais.

## 🔐 Ransomware Simulado: Conceitos e Fluxo
- **Preparação segura**: Uso exclusivo de arquivos fictícios de teste dentro de um diretório isolado (`lab_teste/`), sem tocar em arquivos reais ou do sistema.
- **Ciclo de criptografia e recuperação**:
  1. Criação de arquivos de teste com conteúdo fictício.
  2. Geração de chave de criptografia para o laboratório.
  3. Criptografia dos arquivos de teste e geração de um arquivo de instrução/resgate simulado (`LEIA_RECUPERACAO.txt`).
  4. Processo de descriptografia utilizando a chave gerada para restaurar o conteúdo original.
- **Lição central**: Sem chave segura ou sem cópia de recuperação íntegra (como *backup offline* ou *snapshot* protegido), a recuperação de dados torna-se crítica.

## ⌨️ Keylogger Simulado: Conceitos, Furtividade e Envio
- **Captura em arquivo `.txt`**: Compreensão de como eventos de teclado podem ser registrados sequencialmente em um arquivo de log em ambiente de teste.
- **Furtividade (*stealth*)**: Estudo de como processos tentam reduzir visibilidade (execução silenciosa, nomes genéricos) e como a defesa identifica esses padrões por comportamento, processos em execução e acesso a *hooks*/arquivos.
- **Envio automático (exfiltração simulada)**: Análise do risco quando dados capturados são enviados automaticamente por canais externos (como e-mail), destacando a importância de controles de rede, autenticação de contas e detecção de anomalias.

## 🛡️ Reflexão sobre Defesa e Mitigação
- **Backups resilientes (regra 3-2-1 e isolamento)**: Manter cópias fora do alcance direto de alterações/criptografia indevida e testar restaurações periodicamente.
- **Antivírus e EDR**: Detecção baseada em assinatura, heurística e comportamento (ex.: alterações em massa de arquivos, execução suspeita ou padrões de *keylogging*).
- **Firewall e controle de rede**: Restringir conexões de saída não autorizadas e limitar portas/serviços expostos.
- **Sandboxing e isolamento**: Executar arquivos ou anexos duvidosos em ambientes isolados antes de confiar neles.
- **Conscientização e menor privilégio**: Treinamento contínuo contra *phishing*/downloads duvidosos, uso de MFA e contas com o mínimo de privilégio necessário.

## ⚠️ Aviso Ético
Este material tem finalidade **exclusivamente educacional e defensiva**. Qualquer prática ou teste deve ocorrer apenas em ambientes próprios, isolados e autorizados.

