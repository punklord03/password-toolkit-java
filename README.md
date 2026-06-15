# password-toolkit-java
Java utility for generating secure passwords and evaluating password strength.



import java.util.Random;
import java.util.Scanner;

public class PasswordToolkit {

    public static String generatePassword(int length) {
        String chars =
                "ABCDEFGHIJKLMNOPQRSTUVWXYZ" +
                "abcdefghijklmnopqrstuvwxyz" +
                "0123456789" +
                "!@#$%^&*";

        Random random = new Random();
        StringBuilder password = new StringBuilder();

        for (int i = 0; i < length; i++) {
            password.append(chars.charAt(
                    random.nextInt(chars.length())));
        }

        return password.toString();
    }

    public static void checkStrength(String password) {

        boolean upper = false;
        boolean lower = false;
        boolean digit = false;
        boolean special = false;

        for (char c : password.toCharArray()) {

            if (Character.isUpperCase(c))
                upper = true;

            else if (Character.isLowerCase(c))
                lower = true;

            else if (Character.isDigit(c))
                digit = true;

            else
                special = true;
        }

        int score = 0;

        if (upper) score++;
        if (lower) score++;
        if (digit) score++;
        if (special) score++;

        if (password.length() >= 8) score++;

        System.out.println("\nPassword Score: " + score + "/5");

        if (score <= 2)
            System.out.println("Weak Password");

        else if (score <= 4)
            System.out.println("Medium Password");

        else
            System.out.println("Strong Password");
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.println("=== Password Toolkit ===");
        System.out.println("1. Generate Password");
        System.out.println("2. Check Password Strength");

        int choice = sc.nextInt();

        switch (choice) {

            case 1:
                System.out.print("Enter Password Length: ");
                int length = sc.nextInt();

                String password = generatePassword(length);

                System.out.println("Generated Password:");
                System.out.println(password);
                break;

            case 2:
                sc.nextLine();

                System.out.print("Enter Password: ");
                String pass = sc.nextLine();

                checkStrength(pass);
                break;

            default:
                System.out.println("Invalid Choice");
        }
    }
}
