# hello-world
The first steps
Hi peopls!
I like Java, I am starting study, it will be funny and well.
I like sailing.
//class main
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class StartCalculator {

    public static void main(String[] args)  {
         Instruction.printInstruction();//Виводимо іструкцію користувача.

         CalculatorEngineer calculatorEngineer = new CalculatorEngineer();/*Задаємо екземпляр класу
    для визову метода який обробляє вводні дані.*/

//  медод визиваемо в блоці де можна викинути та обробити виключення.
        try {
            calculatorEngineer.goCount();
        } catch (Exception e) {
            System.out.println("Sorry! Try again.");
//            закриваємо від користувача StakeTrace.
//            e.printStackTrace();
        }
    }
}

//instruction
public class Instruction {

    public static void printInstruction(){
        System.out.println("Hello!" +
                "To perform a mathematical action, enter the first number," +
                " then the space, then the mathematical sign of the action,");
        System.out.println(" again the space and the second number, press Enter.");
        System.out.println("Pay attention to the spaces and perform actions with Roman numerals only from I to X.");
        System.out.println();
        System.out.println("Для виконнання математичної дії введіть перше число, потім пробіл," +
                "потім математичний знак дії,");
        System.out.println(" знов пробіл, та друге число, натисніть Enter");
        System.out.println("Приділяйте увагу до пробілів і виконуйте дії з римськими цифрами тільки від I до X.");

    }
}

// engineer class
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class CalculatorEngineer {
    private int a;
    private int b;
    private int c;
    private String operation;

    public void goCount() throws Exception{

        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        String num = reader.readLine(); //Зчитуємо вводні дані та заносимо їх в строку.

        String [] str = num.split(" "); // Розбиваємо строку за пробілом.

//      порівнюем  якщо перша і третя частини сроки є числами int присвоюваєм їх значення нашим змінним.
        if(Character.isDigit(str[0].charAt(0)) && Character.isDigit(str[2].charAt(0))){
            a = Integer.parseInt(str[0]);
            b = Integer.parseInt(str[2]);
            operation = str[1];// присвоюваєм знак операції, перевірка в методі count.
            count();// визиваємо метод обчислювання
            System.out.println(c); //Виводимо результат.
        }
        else {
            NumbersType type1 = new NumbersType(str[0], str[2]);//Задаємо екземпляр для
//          для конвертаціі чисел

            a = type1.conversion1();//конвертуемо в int/
            b = type1.conversion2();
            if(a > 0 && b > 0){
            operation = str[1];

            count();
            String s = NumbersType.toRomanNum(c); //результат конвертуемо у римськи
            System.out.println(s); //Виводимо результат.
            }
            else {
                //Якщо є помилка вводу виводимо пояснення
                System.out.println("Звиняйте, калькулятор маленький, знає тільки від І до Х." +
                        "Спробуйте знову.");
            }
        }

    }
//метод обчислювання котрий визиває методи з іншого класу в залежності від знаку математичної дії.
    public void count(){
        MyMath math = new MyMath();


        switch (operation){
            case "+":
                c = math.nPlus(a, b);

                break;

            case "-":
                c = math.nMinus(a, b);
                break;

            case "*":
                c = math.nMultiply(a, b);
                break;

            case "/":
                c = math.nDivision(a, b);
                break;

                default: //Якщо ввели не коректний символ виводить пояснення
                    System.out.println("Sorry! You are mistaken, try again, please. + - / *");

        }

    }
//class math operations
public class MyMath {

    public int nPlus(int a, int b){
        return a + b;
    }

    public int nMinus(int a, int b){
        return a - b;
    }

    public int nDivision(int a, int b){
        return a / b;
    }

    public int nMultiply(int a, int b){
        return a * b;
    }
}
//class converting arabic numerals to roman and back
public class NumbersType {
    private int x;
    private int y;
    private String st1;
    private String st2;

    public NumbersType(String st1, String st2) {
        this.st1 = st1;
        this.st2 = st2;
    }
//  конвертування римских цифер у арабськи.
    public int conversion1(){

        switch (st1){
            case "I":
                x = 1;
                break;

            case "II":
                x = 2;
                break;

            case "III":
                x = 3;
                break;

            case "IV":
                x = 4;
                break;

            case "V":
                x = 5;
                break;

            case "VI":
                x = 6;
                break;

            case "VII":
                x = 7;
                break;

            case "VIII":
                x = 8;
                break;

            case "IX":
                x = 9;
                break;

            case "X":
                x = 10;
                break;

                default:
                    System.out.println("Невірно введене перше число.");
        }

        return x;
    }

    public int conversion2(){
        switch (st2){
            case "I":
                y = 1;
                break;

            case "II":
                y = 2;
                break;

            case "III":
                 y = 3;
                 break;

            case "IV":
                y = 4;
                break;

            case "V":
                y = 5;
                break;

            case "VI":
                y = 6;
                break;

            case "VII":
                y = 7;
                break;

            case "VIII":
                y = 8;
                break;

            case "IX":
                y = 9;
                break;

            case "X":
                y = 10;
                break;

                default:
                    System.out.println("Невірно введене друге число");
        }
        return y;
    }

//  конвертування арабських у римськи
   protected static String toRomanNum(int n){
        return String.valueOf(new char[n]).replace('\0','I').
                replace("IIIII","V").
                replace("IIII","IV").
                replace("VV", "X").
                replace("VIV","IX").
                replace("XXXXX", "L").
                replace("XXXX", "XL").
                replace("LL","C").
                replace("LXL", "XC").
                replace("CCCCC", "D").
                replace("CCCC", "CD").
                replace("DD", "M").
                replace("DCD","CM");

   }
   
}

Тестове завдання на Java

Написати программу “Калькулятор“
Обов’язкові вимоги

    Калькулятор command line application. Користувач запускає його з консолі і вводить дані через консоль.
    Калькулятор вміє виконувати операції додавання, віднімання, множення та ділення з двома числами:
        a + b, a - b, a * b, a / b
    Калькулятор вміє працювати з арабськими і римськими числами. Вираз містить числа одного типу: II + 2 - не валідний вираз.
    Калькулятор працює з цілими числами.
    Калькулятор вміє працювати з арабськими числами від 0 до 10. З римськими числами від І до X.
    Зверни увагу на правила ООП. Обдумай структуру класів. Завдання в яких весь код в одному класі будуть оцінені низько.

НЕ обов’язкові вимоги

    Обробка виразів з декількома операціями - НЕ обов’язкова.
    Обробка чисел більше 10 - НЕ обов’язкова.
