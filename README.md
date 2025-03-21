# Declara-o-de-Imposto-de-Renda
Declarar o imposto para o Leão Malvado

def calcular_irpf(rendimento_bruto, deducoes, imposto_retido):
    # Base de cálculo após deduções
    base_calculo = max(rendimento_bruto - deducoes, 0)
    
    # Tabelas de alíquotas e deduções de 2024 (valores aproximados)
    faixas = [2112, 2826.65, 3751.05, 4664.68]
    aliquotas = [0, 7.5, 15, 22.5, 27.5]
    deducoes_faixas = [0, 158.40, 370.40, 651.73, 884.96]
    
    # Cálculo do imposto devido
    if base_calculo <= faixas[0]:
        imposto_devido = 0
    elif base_calculo <= faixas[1]:
        imposto_devido = (base_calculo * (aliquotas[1] / 100)) - deducoes_faixas[1]
    elif base_calculo <= faixas[2]:
        imposto_devido = (base_calculo * (aliquotas[2] / 100)) - deducoes_faixas[2]
    elif base_calculo <= faixas[3]:
        imposto_devido = (base_calculo * (aliquotas[3] / 100)) - deducoes_faixas[3]
    else:
        imposto_devido = (base_calculo * (aliquotas[4] / 100)) - deducoes_faixas[4]
    
    # Verifica se há imposto a pagar ou restituição
    saldo = imposto_devido - imposto_retido
    
    return imposto_devido, saldo

# Exemplo de uso
def main():
    rendimento_bruto = float(input("Digite seu rendimento bruto anual: R$ "))
    deducoes = float(input("Digite o total de deduções permitidas: R$ "))
    imposto_retido = float(input("Digite o total de imposto já retido na fonte: R$ "))
    
    imposto_devido, saldo = calcular_irpf(rendimento_bruto, deducoes, imposto_retido)
    
    print(f"Imposto devido: R$ {imposto_devido:.2f}")
    if saldo > 0:
        print(f"Você precisa pagar: R$ {saldo:.2f}")
    else:
        print(f"Você tem restituição de: R$ {-saldo:.2f}")

if __name__ == "__main__":
    main()

