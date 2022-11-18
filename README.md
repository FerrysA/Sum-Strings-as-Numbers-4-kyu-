# Sum_Strings_as-Numbers
# 18.11.2022
# Сложение больших чисел, используя представление чисел в виде строки
# ссылка на задание
# Код:
``` java
   public static String sumStrings(String a, String b) {
        int n = a.length();
        int m = b.length();
        int k = 0;
        String res = "";
        int vume = 0;
        int x = 0;
        int y = 0;
        int z = 0;
        int zres = 0;
        int min = Math.min(n, m);


        for (int i = 1; i <= min; i++) {
            x = Character.digit(a.charAt(n - i), 10);
            y = Character.digit(b.charAt(m - i), 10);
            z = x + y;
            res += (z + vume) % 10;
            vume = (z + vume) / 10;

        }
        if (n > m) {
            for (int i = m + 1; i <= n; i++) {
                x = Character.digit(a.charAt(n - i), 10);
                y = 0;
                z = x + y;
                res += (z + vume) % 10;
                vume = (z + vume) / 10;

            }

        }
        if (m > n) {
            for (int i = n + 1; i <= m; i++) {
                y = Character.digit(b.charAt(m - i), 10);
                x = 0;
                z = x + y;

                res += (z + vume) % 10;
                vume = (z + vume) / 10;

            }

        }
        if (vume == 1) {
            res += vume;
        }

        String tmp = res;
        k = res.length();
        res = "";
        int cont = 0;
        for (int i = 0; i < k; i++) {
            if (tmp.charAt(k - i - 1) == '0' && cont == 0) {
                continue;
            }
            cont = 1;
            res += Character.toString(tmp.charAt(k - i - 1));

        }

        return res;
    }
```
понравивщееся решение (автор groskowski)
```java
public static String sumStrings(String aa, String bb) {
    char[] a = aa.replaceFirst("^0+(?!$)", "").toCharArray(), b = bb.replaceFirst("^0+(?!$)", "").toCharArray();
    int carry = 0; StringBuilder sb = new StringBuilder();
    int minL = Math.min(a.length, b.length), maxL = Math.max(a.length, b.length);
    for(int i = maxL - 1; i >= 0; i--){
      int ca = (i + a.length - maxL >= 0 ? a[i + a.length - maxL] : '0') - '0';
      int cb = (i + b.length - maxL >= 0 ? b[i + b.length - maxL] : '0') - '0';
      int s = ca + cb + carry;
      carry = s / 10;
      s %= 10;
      sb.append(s);
    }
    return sb.append(carry != 0 ? carry : "").reverse().toString();
  }
