```sql
SELECT * FROM log_alteracoes;
```

Se tudo estiver certo, a saída mostrará que o **campo `titulo` foi alterado**, incluindo o **valor antigo** (`O Senhor dos Anéis`) e o **novo** (`O Hobbit`).

---

# 📌 Como Excluir um Trigger?

Se precisar excluir o trigger, use:

```sql
DROP TRIGGER tr_log_alteracoes_livros;
```

---

# 🔥 Conclusão

✅ O trigger monitora alterações na tabela `livros` e registra mudanças na tabela `log_alteracoes`.  
✅ Para testar, **atualize um registro** e depois consulte `log_alteracoes`.  
✅ Para ver os triggers existentes, use `SHOW TRIGGERS FROM biblioteca;`.