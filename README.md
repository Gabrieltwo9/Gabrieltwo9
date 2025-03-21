import java.util.Random;
import java.util.Scanner;

public class GeradorCartaoCredito {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Escolha a bandeira do cartão:");
        System.out.println("1 - Visa (16 dígitos)");
        System.out.println("2 - MasterCard (16 dígitos)");
        System.out.println("3 - American Express (15 dígitos)");
        System.out.print("Opção: ");

        int escolha = scanner.nextInt();
        String prefixo;
        int tamanho;

        switch (escolha) {
            case 1:
                prefixo = "4";  // Visa começa com 4
                tamanho = 16;
                break;
            case 2:
                prefixo = "51"; // MasterCard começa com 51-55
                tamanho = 16;
                break;
            case 3:
                prefixo = "34"; // American Express começa com 34 ou 37
                tamanho = 15;
                break;
            default:
                System.out.println("Opção inválida!");
                scanner.close();
                return;
        }

        String numeroCartao = gerarCartao(prefixo, tamanho);
        System.out.println("Número do Cartão Gerado: " + numeroCartao);

        scanner.close();
    }

    // Método para gerar um número de cartão válido
    public static String gerarCartao(String prefixo, int tamanho) {
        Random random = new Random();
        StringBuilder numeroCartao = new StringBuilder(prefixo);

        // Gera os primeiros dígitos aleatórios até o penúltimo
        while (numeroCartao.length() < tamanho - 1) {
            numeroCartao.append(random.nextInt(10));
        }

        // Calcula o dígito verificador usando o Algoritmo de Luhn
        int digitoVerificador = calcularDigitoLuhn(numeroCartao.toString());
        numeroCartao.append(digitoVerificador);

        return numeroCartao.toString();
    }

    // Implementação do Algoritmo de Luhn
    private static int calcularDigitoLuhn(String numeroParcial) {
        int soma = 0;
        boolean dobrar = true;

        // Percorre os dígitos de trás para frente
        for (int i = numeroParcial.length() - 1; i >= 0; i--) {
            int digito = Character.getNumericValue(numeroParcial.charAt(i));
            if (dobrar) {
                digito *= 2;
                if (digito > 9) digito -= 9;
            }
            soma += digito;
            dobrar = !dobrar;
        }

        // Calcula o último dígito
        return (10 - (soma % 10)) % 10;
    }
}
<!---
Gabrieltwo9/Gabrieltwo9 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
