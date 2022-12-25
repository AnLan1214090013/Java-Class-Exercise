# Java-Class-Exercise
Java网页题答案

1021

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

    public class Main {
        public static void main(String[] args){
            Scanner sc = new Scanner(System.in);
            String original = sc.nextLine();
            int n = original.length();
            List<Data> disposed = new ArrayList<>();
            char s = ' ';
            for(int i=0;i<n;i++){
                s = original.charAt(i);
                if(s >= 'a' && s <= 'z'){
                    Data data = new Data((char)(s-'a'+'A'), i);
                    disposed.add(data);
                } else if (s >= 'A' && s <= 'Z') {
                    Data data = new Data(s, i);
                    disposed.add(data);
                }
            }
            int dL = disposed.size();
            int maxL = 0;
            int index0 = 0;
            int index1 = 0;
            int p0, p1;
            for(int j=1;j<dL-1;j++){
                if(disposed.get(j).ch == disposed.get(j-1).ch){
                    p0 = j-1;
                    p1 = j;
                } else if (disposed.get(j).ch == disposed.get(j+1).ch) {
                    p0 = j;
                    p1 = j+1;
                } else if (disposed.get(j-1).ch == disposed.get(j+1).ch) {
                    p0 = j-1;
                    p1 = j+1;
                } else{
                    continue;
                }
                int temL = 0;
                while(true){
                    p0--;
                    p1++;
                    if(p0 < 0 || p1>=dL){
                        break;
                    }
                    if(disposed.get(p0).ch == disposed.get(p1).ch){
                        temL++;
                    }else{
                        break;
                    }
                }
                if(temL > maxL){
                    maxL = temL;
                    index0 = p0 + 1;
                    index1 = p1 - 1;
                }
            }
            System.out.println(original.substring(disposed.get(index0).index, disposed.get(index1).index+1));
        }
    }
    class Data{
        public char ch;
        public int index;
        public Data(char ch, int index){
            this.ch = ch;
            this.index = index;
        }
        public Data(){}
}

1035
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()) {
            int t = sc.nextInt();
            for (int i = 0; i < t; i++) {
                int a = 0;
                String str = sc.next();
                int n = sc.nextInt();
                for (int j = 0; j < str.length(); j++) {
                    if (str.charAt(j) == '.') {
                        a = j;
                    }
                }
                if (str.length() > (a + n))
                    System.out.println(str.charAt(a + n));
                else System.out.println('0');
            }
        }
        sc.close();
        }
}

1016
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()) {
            int m = sc.nextInt();
            boolean flag =true;
            inner:
                for (int i = 1; i <= m; i++) {
                    for (int j = 1; j <= m; j++) {
                        for (int k = 1; k <= m; k++) {
                            if (isPrime(i) && isPrime(j) && isPrime(k) && (i + j + k == m) && (i <= j) && (j <= k))
                            { System.out.println(i + " " + j + " " + k);
                           flag = false;
                               if(flag == false){  break inner;}
                            }
                        }
                    }
                }
        }
    }
    public static boolean isPrime(int i) {
        int n;
        boolean flag = true;
        if (1 == i)
            flag = false;
        for (n = 2; n <= i - 1; n++)
            if (i % n == 0) {
                flag = false;
                break;
            }
        return flag;
    }


}

1019
import java.util.Scanner;
public class Main {
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    while (sc.hasNext()) {
        int m = sc.nextInt();
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= m; j++) {
                if (isPrime(i) && isPrime(j) && (i + j == m) && (i <= j)) {
                    System.out.println(m + "=" + i + "+" + j);
                }
            }
        }
    }
}
public static boolean isPrime(int i) {
    int n;
    boolean flag = true;
    if (1 == i)                        
        flag = false;
    for (n = 2; n <= i - 1; n++)        
        if (i % n == 0) {
            flag = false;
            break;
        }
    return flag;
}
}

1036
import java.io.IOException;
import java.util.Scanner;

public class Main {

    public static int ans;

    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()){
            ans = 0;
            String s = sc.nextLine();
            for (int i = 0; i < s.length(); i++) {
                //考虑两种情况：aba 和 abba
                centerSpread(s, i, i);
                centerSpread(s, i, i + 1);
            }
            System.out.println(ans);
        }

    }

    //判断回文串的中心扩散法
    private static void centerSpread(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
            ans++;
        }
    }

    //方法二：动态规划
    private static int dp(String s) {
        int n = s.length(), ans = 0;
        boolean[][] dp = new boolean[n][n];
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i; j < n; j++) {
                dp[i][j] = (s.charAt(i) == s.charAt(j)) && (j - i <= 2 || dp[i + 1][j - 1]);
                if (dp[i][j]) ans++;
            }
        }
        return ans;
    }
}

1023
import java.math.BigInteger;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Integer num = null;
        try {
            num = Integer.parseInt(sc.nextLine());
        } catch (NumberFormatException e) {
            throw new RuntimeException("请输入数字");
        } catch (Exception e) {
            e.printStackTrace();
        }
        if (num < 0) {
            throw new RuntimeException("输入大于等于0的数据");
        }
        if (num > 15) {
            System.out.println(getBigFac(num));
            return;
        }
        System.out.println(getFac(num));
    }

    public static long getFac(Integer n) {
        if (n == 1) {
            return 1;
        }
        return getFac(n - 1) * n;
    }

    public static BigInteger getBigFac(Integer n) {
        BigInteger num = new BigInteger("1");
        for (int i = 1; i <= n; i++) {
            num = num.multiply(new BigInteger(i + ""));
        }
        return num;


    }
}

1017
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner= new  Scanner(System.in);
        while(scanner.hasNext()) {
            int num = scanner.nextInt();
            print(num);
        }
        scanner.close();
    }

    public static void print(int n) {

        int i;
        System.out.printf(n+"=");
        for(i=2;i<=n;i++)//遍历从2到本身的所有数
        {
            while(n%i==0)//能整除
            {
                System.out.printf(i+""); //则这个数为其中一个质数
                n/=i;//n就除去i，变成一个新的数字继续执行
                if(n!=1)
                {
                    System.out.printf("*");
                };//直到n=1
                if(n==1)
                {
                    break;
                }
            }
        }


    }


}

1014
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner= new  Scanner(System.in);
        while(scanner.hasNext()) {
            int num = scanner.nextInt();
            print(num);
        }
        scanner.close();
    }

    public static void print(int num) {

        int a1,a2,M=10007;
        a1=a2=1;
        int sum=0,temp;//sum是保存余数的变量 ，temp是为了方便交换数据
//        long n=1000000;
        for(long i=1;i<=num;i++)
        {
            sum=a1%M;
            temp=a2;
            a2=(a1+a2)%M;
            a1=temp;
        }
        System.out.println(sum);


    }


}

1008
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner= new  Scanner(System.in);
        while(scanner.hasNext()) {
            int num = scanner.nextInt();
            print(num);
        }
        scanner.close();
    }

    public static void print(int num) {

        int[][] matrix = new int[num][num];

        for(int i=0;i< matrix.length;i++){
            matrix[i][0] = 1+i;
            for (int j=0;j<matrix[i].length;j++){
                matrix[i][j] = matrix[i][0]+num*j;
            }
        }

        for(int i=0;i< matrix.length;i++){
            for (int j=0;j<matrix[i].length;j++){
                System.out.printf(matrix[i][j]+"");
                if(j<matrix[i].length-1){
                    System.out.printf(" ");
                }

            }
            System.out.println("");
        }


    }


}

1002
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner= new  Scanner(System.in);
        while(scanner.hasNext()) {
            String date1 = scanner.nextLine();
            String date2 = scanner.nextLine();
            getDiff(date1, date2);
        }
        scanner.close();
    }

    public static void getDiff(String date1, String date2){

        int[][] month = {{0,0},{31,31},{28,29},{31,31},{30,30},{31,31},{30,30},{31,31},{31,31},{30,30},{31,31},{30,30},{31,31}};

        int num1,num2,t,d,sum,y1,m1,d1,y2,m2,d2;
        num1 = Integer.parseInt(date1);
        num2 = Integer.parseInt(date2);

        if(num1>num2) {
            t=num1;
            num1=num2;
            num2=t;
        }
        y1=num1/10000;
        m1=num1/100%100;
        d1=num1%100;
        y2=num2/10000;
        m2=num2/100%100;
        d2=num2%100;
        sum=1;
        while(y2>y1||m2>m1||d2>d1)
        {
            d1++;
            if(d1==month[m1][year(y1)]+1)
            {
                m1++;
                d1=1;
            }
            if(m1==13)
            {
                y1++;
                m1=1;
            }
            sum++;

        }
        System.out.println(sum);
    }

    public static int year(int n){
        if ((n % 4 == 0 && n % 100 != 0) || (n % 400 == 0)) {
            return 1;
        }
        return 0;
    }


}

1007
import java.util.Scanner;
public class Main {
    
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        while(s.hasNext()){
            int N = s.nextInt();
            int M = s.nextInt();
            int a = josephu(N, M);
            System.out.println(a);
        }
    }
    
    public static int josephu(int m,int k){
        int ans = 0;
        int[] arr = new int[m];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = 1;
        }
        int count = 0,num = 0;
        for (int i = 0; i <= arr.length; i++) {
            if (i == arr.length) {
                i = -1;
                continue;
            }
            if (arr[i] == 1){
                //有效元素
                ++count;
                if (count == k){//爆炸
                    arr[i] = 0;
                    ++num;//死亡数+1
                    count = 0;//重置计数器
                }
            }
            if (num == m-1){//只剩一个人
                for (int j = 0; j < arr.length; j++) {
                    if (arr[j] == 1){
                        return j+1;
                    }
                }
            }
        }
        return ans;//ans是j+1

    }

    
}

1000
import java.math.BigDecimal;
import java.util.*;
public class Main{     
    public static  void main(String[] args)  {   
        Scanner cin = new Scanner(System.in);             
        while(cin.hasNext()){
            int m=cin.nextInt();
        
            for(int i=0;i<m;i++){
            BigDecimal b1=cin.nextBigDecimal();
            BigDecimal b2=cin.nextBigDecimal();
            BigDecimal c=b1.add(b2).stripTrailingZeros();
             String str = c.toPlainString();
             if (str.indexOf('.') == -1) str += ".0";
             System.out.println(str);          
            }
     }
        cin.close();  
    }  
}

1024
import java.math.BigDecimal;    
import java.util.*;    
    
public class Main {    
    public static void main(String args[]){    
        Scanner cin = new Scanner(System.in);    
        BigDecimal a,b,c; 
        while(cin.hasNext())
        {
            a = cin.nextBigDecimal();
            b = cin.nextBigDecimal();
            c = a.add(b);
            if(c.compareTo(BigDecimal.ZERO)==0)
            {
                System.out.println("0");
            }
            else
            {
                System.out.println(c.stripTrailingZeros().toPlainString());
            }
        }
    } 
}

1025
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner= new  Scanner(System.in);
        while(scanner.hasNext()) {
            int a = scanner.nextInt();
            int b = scanner.nextInt();
            System.out.println(a+b);
        }
        scanner.close();

    }
}
