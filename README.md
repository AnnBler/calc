import java.io.IOException;
import java.util.Scanner;

class Main {
    static String calc(String input) throws IOException {
        String[] parts = input.split(" ");
        

        if (parts.length != 3) {
            throw new IOException("формат математической операции не удовлетворяет заданию - два операнда и один оператор (+, -, /, *)");

        }


        int a, b; // Объявляет переменные для чисел.
        try {
            a = Integer.parseInt(parts[0]);
            b = Integer.parseInt(parts[2]);
            if (a < 1 || a > 10 || b < 1 || b > 10) {
                throw new IOException("Числа должны быть от 1 до 10 включительно.");
            }
        } catch (IOException e) {
            throw new IOException("Некорректные числа, т.к числа должны быть от 1 до 10 включительно.");
        }

        int result;
        switch (parts[1]) {
            case "+":
                result = a + b;
                break;
            case "-":
                result = a - b;
                break;
            case "*":
                result = a * b;
                break;
            case "/":
                if (b == 0) {
                    throw new IOException("Деление на ноль");
                }
                result = a / b;
                break;
            default:
                throw new IOException("Некорректная операция");
        }

        return String.valueOf(result); // Возвращает результат операции в виде строки.
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите арифметическое выражение (например, 2 + 3): ");
        String input = scanner.nextLine();

        try {
            String result = calc(input);
            System.out.println("Результат: " + result);
        } catch (IOException e) {
            System.out.println("Ошибка: " + e.getMessage()); // Пытается вычислить результат выражения, используя метод calc. Если происходит ошибка, выводит сообщение об ошибке.
        }

        scanner.close();
    }
}
