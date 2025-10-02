# IA — Machine Learning | Perceptron & MLP  
**Disciplina:** Inteligência Artificial — Prof. Claudinei Dias (Ney)  
**Atividade:** Portas lógicas AND/OR com Perceptron (x₃ = −1 como viés), Regra Delta e versão com scikit-learn; caso extra XOR com MLP  
**Alunos:** **Alberto Zilio** · **Roni Pereira**  
**Data:** 02/10/2025

---

## Sumário
1. Objetivo  
2. Dados e Codificação  
3. Perceptron (Regra Clássica) — AND e OR  
4. Fronteira de Decisão e Interpretação dos Pesos  
5. Curvas de Erro, Taxa de Aprendizado (η) e Efeito do *Shuffle*  
6. Perceptron com **Regra Delta** (saída bipolar)  
7. Repetição com **scikit-learn**  
8. (Opcional) XOR — Limite do Perceptron e Solução com **MLP**  
9. Conclusões  
10. Referências

---

## 1) Objetivo
Implementar, analisar e comparar classificadores lineares do tipo **Perceptron** para resolver as portas lógicas **AND** e **OR** utilizando:
- **Regra de atualização clássica** (atualiza apenas quando erra);  
- **Regra Delta** (aprendizado por gradiente com saída bipolar);  
- **Versão com scikit-learn**.  

Como extensão, mostrar o **limite do Perceptron** no caso **XOR** e resolvê-lo com uma **MLP**.

---

## 2) Dados e Codificação
- Entradas em \{-1, +1\}: \(x_1, x_2 \in \{-1,+1\}\).  
- Viés explícito como terceira entrada fixa \(x_3 = -1\) (equivale a intercepto).  
- Saída desejada \(d \in \{-1, +1\}\).

**Tabelas verdade (bipolar):**
- **OR**: \[(+1,+1)\to+1,\ (+1,-1)\to+1,\ (-1,+1)\to+1,\ (-1,-1)\to-1\]  
- **AND**: \[(+1,+1)\to+1,\ (+1,-1)\to-1,\ (-1,+1)\to-1,\ (-1,-1)\to-1\]

---

## 3) Perceptron (Regra Clássica) — AND e OR
**Ativação:** degrau: \(\hat y = \mathrm{{sign}}(u)\), com \(u = \mathbf{{w}}^\top \mathbf{{x}}\).  
**Regra de atualização (apenas em erro):**  
\[
\mathbf{{w}} \leftarrow \mathbf{{w}} + \eta \, d \, \mathbf{{x}}
\]

**Resultados:** Convergência rápida e acurácia 100% em OR e AND.

---

## 4) Fronteira de Decisão e Interpretação dos Pesos
Com \(x_3=-1\):  
\[
w_1 x_1 + w_2 x_2 + w_3(-1) = 0 
\;\Rightarrow\;
x_2 = \frac{w_3 - w_1 x_1}{w_2} \; (w_2 \neq 0)
\]

**Viés/pesos:** \(w_1, w_2\) moldam a inclinação; \(w_3\) desloca a reta.


---

## 5) Curvas de Erro, η e *Shuffle*
**Achados:**
- η pequeno → mais épocas; η moderado (0.5–1.0) → bom custo/benefício; η alto (2.0) pode oscilar.  
- *Shuffle* tende a acelerar/estabilizar a convergência.


---

## 6) Regra Delta (saída bipolar)
Usamos \( o = 2/(1+e^{-\lambda u}) - 1 \) e derivada \( (1-o^2)/2 \).  
**SSE** decresce até o limiar; acurácia 100% por sinal(o).



---

## 7) Repetição com scikit-learn (Perceptron)
`fit_intercept=True` trata o viés internamente. Resultados equivalentes (acurácia 100%).


---

## 8) (Opcional) XOR — Limite do Perceptron e MLP
Perceptron linear falha; MLP (tanh, 1 camada oculta) separa perfeitamente.


---

## 9) Conclusões
- **AND/OR**: separáveis linearmente → Perceptron (clássico) e Delta convergem (100%).  
- **Parâmetros** (η, shuffle) influenciam eficiência.  
- **scikit-learn** confirma resultados.  
- **XOR** destaca limite do linear; **MLP** resolve com não-linearidade.

---

## 10) Referências
- PDF da atividade — Perceptron, Regra Delta e exercícios AND/OR/XOR.  
- Bishop, C. *Pattern Recognition and Machine Learning*. Springer, 2006.  
- scikit-learn: Pedregosa et al., *JMLR* 12 (2011), 2825–2830.
