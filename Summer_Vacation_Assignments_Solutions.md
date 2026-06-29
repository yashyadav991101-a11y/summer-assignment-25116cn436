## Day 1

### Q1. Calculate sum of first N natural numbers

**Logic:** Loop from 1 to N, adding each value. Alternatively: `sum = n*(n+1)/2`.

```c
#include <stdio.h>

int main() {
    int n, sum = 0;
    printf("Enter N: ");
    scanf("%d", &n);
    for (int i = 1; i <= n; i++)
        sum += i;
    printf("Sum = %d\n", sum);
    return 0;
}
```

---

### Q2. Print multiplication table of a given number

**Logic:** Loop from 1 to 10 and print `n*i` each iteration.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    for (int i = 1; i <= 10; i++)
        printf("%d x %d = %d\n", n, i, n * i);
    return 0;
}
```

---

### Q3. Find factorial of a number

**Logic:** Multiply from 2 to n. Use `long long` for large values.

```c
#include <stdio.h>

int main() {
    int n;
    long long fact = 1;
    printf("Enter n: ");
    scanf("%d", &n);
    for (int i = 2; i <= n; i++)
        fact *= i;
    printf("Factorial = %lld\n", fact);
    return 0;
}
```

---

### Q4. Count digits in a number

**Logic:** Divide by 10 repeatedly and count iterations until n becomes 0.

```c
#include <stdio.h>

int main() {
    int n, count = 0;
    printf("Enter number: ");
    scanf("%d", &n);
    if (n == 0) { printf("Digits = 1\n"); return 0; }
    if (n < 0) n = -n;
    while (n > 0) { n /= 10; count++; }
    printf("Digits = %d\n", count);
    return 0;
}
```

---

## Day 2

### Q5. Find sum of digits of a number

**Logic:** Extract last digit with `% 10`, add to sum, remove it with `/ 10`.

```c
#include <stdio.h>

int main() {
    int n, sum = 0;
    printf("Enter number: ");
    scanf("%d", &n);
    if (n < 0) n = -n;
    while (n > 0) { sum += n % 10; n /= 10; }
    printf("Sum of digits = %d\n", sum);
    return 0;
}
```

---

### Q6. Reverse a number

**Logic:** Build the reversed number by shifting digits left (multiply by 10) and adding last digit.

```c
#include <stdio.h>

int main() {
    int n, rev = 0;
    printf("Enter number: ");
    scanf("%d", &n);
    while (n != 0) { rev = rev * 10 + n % 10; n /= 10; }
    printf("Reversed = %d\n", rev);
    return 0;
}
```

---

### Q7. Find product of digits

**Logic:** Same as digit sum but multiply instead of add.

```c
#include <stdio.h>

int main() {
    int n;
    long long prod = 1;
    printf("Enter number: ");
    scanf("%d", &n);
    if (n < 0) n = -n;
    while (n > 0) { prod *= n % 10; n /= 10; }
    printf("Product = %lld\n", prod);
    return 0;
}
```

---

### Q8. Check whether a number is palindrome

**Logic:** Reverse the number and compare with original. If equal, it's a palindrome.

```c
#include <stdio.h>

int main() {
    int n, rev = 0, orig;
    printf("Enter number: ");
    scanf("%d", &n);
    orig = n;
    while (n > 0) { rev = rev * 10 + n % 10; n /= 10; }
    printf(orig == rev ? "Palindrome\n" : "Not Palindrome\n");
    return 0;
}
```

---

## Day 3

### Q9. Check whether a number is prime

**Logic:** Check divisibility from 2 to `sqrt(n)`. If any factor found, not prime.

```c
#include <stdio.h>
#include <math.h>

int main() {
    int n, prime = 1;
    printf("Enter number: ");
    scanf("%d", &n);
    if (n < 2) prime = 0;
    for (int i = 2; i <= sqrt(n) && prime; i++)
        if (n % i == 0) prime = 0;
    printf(prime ? "Prime\n" : "Not Prime\n");
    return 0;
}
```

---

### Q10. Print prime numbers in a range

**Logic:** Use a helper `isPrime()` function and iterate through the range.

```c
#include <stdio.h>
#include <math.h>

int isPrime(int n) {
    if (n < 2) return 0;
    for (int i = 2; i <= sqrt(n); i++)
        if (n % i == 0) return 0;
    return 1;
}

int main() {
    int a, b;
    printf("Enter range (a b): ");
    scanf("%d %d", &a, &b);
    for (int i = a; i <= b; i++)
        if (isPrime(i)) printf("%d ", i);
    printf("\n");
    return 0;
}
```

---

### Q11. Find GCD of two numbers

**Logic:** Euclidean algorithm: `GCD(a, b) = GCD(b, a%b)` until b becomes 0.

```c
#include <stdio.h>

int main() {
    int a, b;
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    while (b != 0) { int t = b; b = a % b; a = t; }
    printf("GCD = %d\n", a);
    return 0;
}
```

---

### Q12. Find LCM of two numbers

**Logic:** `LCM(a,b) = (a / GCD(a,b)) * b`. Divide first to avoid overflow.

```c
#include <stdio.h>

int gcd(int a, int b) { return b == 0 ? a : gcd(b, a % b); }

int main() {
    int a, b;
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    printf("LCM = %d\n", (a / gcd(a, b)) * b);
    return 0;
}
```

---

## Day 4

### Q13. Generate Fibonacci series

**Logic:** Start with 0 and 1. Each term is the sum of the previous two.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter terms: ");
    scanf("%d", &n);
    long long a = 0, b = 1;
    for (int i = 0; i < n; i++) {
        printf("%lld ", a);
        long long t = a + b;
        a = b; b = t;
    }
    printf("\n");
    return 0;
}
```

---

### Q14. Find nth Fibonacci term

**Logic:** Iterate n-1 times to reach the nth term.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter n: ");
    scanf("%d", &n);
    long long a = 0, b = 1;
    if (n == 1) { printf("F(%d) = 0\n", n); return 0; }
    for (int i = 2; i < n; i++) { long long t = a + b; a = b; b = t; }
    printf("F(%d) = %lld\n", n, b);
    return 0;
}
```

---

### Q15. Check Armstrong number

**Logic:** An Armstrong number equals the sum of its digits raised to the power of the number of digits.

```c
#include <stdio.h>
#include <math.h>

int main() {
    int n, orig, sum = 0, digits = 0, temp;
    printf("Enter number: ");
    scanf("%d", &n);
    orig = n; temp = n;
    while (temp > 0) { digits++; temp /= 10; }
    temp = n;
    while (temp > 0) { sum += pow(temp % 10, digits); temp /= 10; }
    printf(sum == orig ? "Armstrong\n" : "Not Armstrong\n");
    return 0;
}
```

---

### Q16. Print Armstrong numbers in a range

**Logic:** Check each number in the range using the `isArmstrong` helper.

```c
#include <stdio.h>
#include <math.h>

int isArmstrong(int n) {
    int temp = n, sum = 0, digits = 0;
    while (temp > 0) { digits++; temp /= 10; }
    temp = n;
    while (temp > 0) { sum += pow(temp % 10, digits); temp /= 10; }
    return sum == n;
}

int main() {
    int a, b;
    printf("Enter range (a b): ");
    scanf("%d %d", &a, &b);
    for (int i = a; i <= b; i++)
        if (isArmstrong(i)) printf("%d ", i);
    printf("\n");
    return 0;
}
```

---

## Day 5

### Q17. Check perfect number

**Logic:** A perfect number equals the sum of its proper divisors (e.g., 6 = 1+2+3).

```c
#include <stdio.h>

int main() {
    int n, sum = 0;
    printf("Enter number: ");
    scanf("%d", &n);
    for (int i = 1; i < n; i++)
        if (n % i == 0) sum += i;
    printf(sum == n ? "Perfect Number\n" : "Not Perfect\n");
    return 0;
}
```

---

### Q18. Check strong number

**Logic:** A strong number equals the sum of factorials of its digits (e.g., 145 = 1!+4!+5!).

```c
#include <stdio.h>

int main() {
    int n, temp, sum = 0;
    printf("Enter number: ");
    scanf("%d", &n);
    temp = n;
    while (temp > 0) {
        int d = temp % 10, fact = 1;
        for (int i = 2; i <= d; i++) fact *= i;
        sum += fact;
        temp /= 10;
    }
    printf(sum == n ? "Strong Number\n" : "Not Strong\n");
    return 0;
}
```

---

### Q19. Print factors of a number

**Logic:** Iterate from 1 to n and print every divisor.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    printf("Factors: ");
    for (int i = 1; i <= n; i++)
        if (n % i == 0) printf("%d ", i);
    printf("\n");
    return 0;
}
```

---

### Q20. Find largest prime factor

**Logic:** Divide out all prime factors starting from 2. The remaining n (if > 2) is itself a prime factor.

```c
#include <stdio.h>

int main() {
    int n, largest = -1;
    printf("Enter number: ");
    scanf("%d", &n);
    while (n % 2 == 0) { largest = 2; n /= 2; }
    for (int i = 3; i * i <= n; i += 2)
        while (n % i == 0) { largest = i; n /= i; }
    if (n > 2) largest = n;
    printf("Largest prime factor = %d\n", largest);
    return 0;
}
```

---

## Day 6

### Q21. Convert decimal to binary

**Logic:** Repeatedly divide by 2 and store remainders, then print in reverse.

```c
#include <stdio.h>

int main() {
    int n, bin[32], i = 0;
    printf("Enter decimal: ");
    scanf("%d", &n);
    while (n > 0) { bin[i++] = n % 2; n /= 2; }
    printf("Binary: ");
    for (int j = i - 1; j >= 0; j--) printf("%d", bin[j]);
    printf("\n");
    return 0;
}
```

---

### Q22. Convert binary to decimal

**Logic:** Process binary digits right-to-left, multiplying each by increasing powers of 2.

```c
#include <stdio.h>

int main() {
    long long bin;
    int dec = 0, base = 1;
    printf("Enter binary: ");
    scanf("%lld", &bin);
    while (bin > 0) { dec += (bin % 10) * base; base *= 2; bin /= 10; }
    printf("Decimal = %d\n", dec);
    return 0;
}
```

---

### Q23. Count set bits in a number

**Logic:** Check the least significant bit using AND with 1, then right-shift. Count when bit is 1.

```c
#include <stdio.h>

int main() {
    int n, count = 0;
    printf("Enter number: ");
    scanf("%d", &n);
    while (n) { count += n & 1; n >>= 1; }
    printf("Set bits = %d\n", count);
    return 0;
}
```

---

### Q24. Find x^n without pow()

**Logic:** Multiply x by itself n times.

```c
#include <stdio.h>

int main() {
    long long x, result = 1;
    int n;
    printf("Enter x and n: ");
    scanf("%lld %d", &x, &n);
    for (int i = 0; i < n; i++) result *= x;
    printf("%lld^%d = %lld\n", x, n, result);
    return 0;
}
```

---

## Day 7

### Q25. Recursive factorial

**Logic:** Base case: `factorial(0) = factorial(1) = 1`. Recursive case: `n * factorial(n-1)`.

```c
#include <stdio.h>

long long factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}

int main() {
    int n;
    printf("Enter n: ");
    scanf("%d", &n);
    printf("Factorial = %lld\n", factorial(n));
    return 0;
}
```

---

### Q26. Recursive Fibonacci

**Logic:** Each call splits into two recursive calls. Note: slow for large n; use memoization for optimization.

```c
#include <stdio.h>

long long fib(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    return fib(n - 1) + fib(n - 2);
}

int main() {
    int n;
    printf("Enter n: ");
    scanf("%d", &n);
    printf("Fib(%d) = %lld\n", n, fib(n));
    return 0;
}
```

---

### Q27. Recursive sum of digits

**Logic:** Add last digit to recursive call on remaining digits.

```c
#include <stdio.h>

int sumDigits(int n) {
    if (n == 0) return 0;
    return n % 10 + sumDigits(n / 10);
}

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    printf("Sum = %d\n", sumDigits(n));
    return 0;
}
```

---

### Q28. Recursive reverse number

**Logic:** Place the last digit at the most significant position using length, then recurse on remaining.

```c
#include <stdio.h>
#include <math.h>

int countDigits(int n) { return (n == 0) ? 0 : 1 + countDigits(n / 10); }

int reverseNum(int n, int len) {
    if (n == 0) return 0;
    return (n % 10) * pow(10, len - 1) + reverseNum(n / 10, len - 1);
}

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    printf("Reversed = %d\n", reverseNum(n, countDigits(n)));
    return 0;
}
```

---

## Day 8

### Q29. Print half pyramid pattern

**Logic:** Each row `i` prints `i` stars.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) printf("* ");
        printf("\n");
    }
    return 0;
}
```

---

### Q30. Print number triangle

**Logic:** Row `i` prints numbers 1 through `i`.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) printf("%d", j);
        printf("\n");
    }
    return 0;
}
```

---

### Q31. Print character triangle

**Logic:** Row `i` prints characters A through (A+i).

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= i; j++) printf("%c", 'A' + j);
        printf("\n");
    }
    return 0;
}
```

---

### Q32. Print repeated-number pattern

**Logic:** Row `i` prints the digit `i` repeated `i` times.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j < i; j++) printf("%d", i);
        printf("\n");
    }
    return 0;
}
```

---

## Day 9

### Q33. Print reverse star pattern

**Logic:** Start from n stars and decrease by 1 each row.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = n; i >= 1; i--) {
        for (int j = 1; j <= i; j++) printf("*");
        printf("\n");
    }
    return 0;
}
```

---

### Q34. Print reverse number triangle

**Logic:** Rows go from n down to 1; each row prints numbers 1 to i.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = n; i >= 1; i--) {
        for (int j = 1; j <= i; j++) printf("%d", j);
        printf("\n");
    }
    return 0;
}
```

---

### Q35. Print repeated character pattern

**Logic:** Row `i` prints the (i+1)th letter of the alphabet (i+1) times.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= i; j++) printf("%c", 'A' + i);
        printf("\n");
    }
    return 0;
}
```

---

### Q36. Print hollow square pattern

**Logic:** Print `*` only on the border (first/last row or first/last column), space inside.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++)
            printf(i==1||i==n||j==1||j==n ? "*" : " ");
        printf("\n");
    }
    return 0;
}
```

---

## Day 10

### Q37. Print star pyramid

**Logic:** Each row `i` has `(n-i)` spaces and `(2i-1)` stars.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n - i; j++) printf(" ");
        for (int j = 1; j <= 2 * i - 1; j++) printf("*");
        printf("\n");
    }
    return 0;
}
```

---

### Q38. Print reverse pyramid

**Logic:** Same logic as star pyramid but iterate from n down to 1.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = n; i >= 1; i--) {
        for (int j = 1; j <= n - i; j++) printf(" ");
        for (int j = 1; j <= 2 * i - 1; j++) printf("*");
        printf("\n");
    }
    return 0;
}
```

---

### Q39. Print number pyramid

**Logic:** Print ascending numbers `1..i` then descending `i-1..1`, centered with spaces.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n - i; j++) printf(" ");
        for (int j = 1; j <= i; j++) printf("%d", j);
        for (int j = i - 1; j >= 1; j--) printf("%d", j);
        printf("\n");
    }
    return 0;
}
```

---

### Q40. Print character pyramid

**Logic:** Similar to number pyramid but using characters A, B, C...

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter rows: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i - 1; j++) printf(" ");
        for (int j = 0; j <= i; j++) printf("%c", 'A' + j);
        for (int j = i - 1; j >= 0; j--) printf("%c", 'A' + j);
        printf("\n");
    }
    return 0;
}
```

---

## Day 11

### Q41. Function to find sum of two numbers

**Logic:** Simple function returning `a + b`.

```c
#include <stdio.h>

int sum(int a, int b) { return a + b; }

int main() {
    int a, b;
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    printf("Sum = %d\n", sum(a, b));
    return 0;
}
```

---

### Q42. Function to find maximum

**Logic:** Use ternary operator to return the larger value.

```c
#include <stdio.h>

int maximum(int a, int b) { return a > b ? a : b; }

int main() {
    int a, b;
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    printf("Max = %d\n", maximum(a, b));
    return 0;
}
```

---

### Q43. Function to check prime

**Logic:** Encapsulates the prime check in a reusable function returning 1 (prime) or 0.

```c
#include <stdio.h>
#include <math.h>

int isPrime(int n) {
    if (n < 2) return 0;
    for (int i = 2; i <= sqrt(n); i++)
        if (n % i == 0) return 0;
    return 1;
}

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    printf(isPrime(n) ? "Prime\n" : "Not Prime\n");
    return 0;
}
```

---

### Q44. Function to find factorial

**Logic:** Iterative factorial function, cleaner and safer than recursive for large n.

```c
#include <stdio.h>

long long factorial(int n) {
    long long f = 1;
    for (int i = 2; i <= n; i++) f *= i;
    return f;
}

int main() {
    int n;
    printf("Enter n: ");
    scanf("%d", &n);
    printf("Factorial = %lld\n", factorial(n));
    return 0;
}
```

---

## Day 12

### Q45. Function for palindrome

**Logic:** Reverses the number and checks equality with original.

```c
#include <stdio.h>

int isPalindrome(int n) {
    int rev = 0, orig = n;
    while (n > 0) { rev = rev * 10 + n % 10; n /= 10; }
    return rev == orig;
}

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    printf(isPalindrome(n) ? "Palindrome\n" : "Not Palindrome\n");
    return 0;
}
```

---

### Q46. Function for Armstrong

**Logic:** Counts digits first, then sums each digit raised to that power.

```c
#include <stdio.h>
#include <math.h>

int isArmstrong(int n) {
    int temp = n, sum = 0, digits = 0;
    while (temp) { digits++; temp /= 10; }
    temp = n;
    while (temp) { sum += pow(temp % 10, digits); temp /= 10; }
    return sum == n;
}

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    printf(isArmstrong(n) ? "Armstrong\n" : "Not Armstrong\n");
    return 0;
}
```

---

### Q47. Function for Fibonacci

**Logic:** Function prints the first n Fibonacci numbers.

```c
#include <stdio.h>

void fibonacci(int n) {
    long long a = 0, b = 1;
    for (int i = 0; i < n; i++) {
        printf("%lld ", a);
        long long t = a + b; a = b; b = t;
    }
    printf("\n");
}

int main() {
    int n;
    printf("Enter terms: ");
    scanf("%d", &n);
    fibonacci(n);
    return 0;
}
```

---

### Q48. Function for perfect number

**Logic:** Sums proper divisors and compares with the number.

```c
#include <stdio.h>

int isPerfect(int n) {
    int sum = 0;
    for (int i = 1; i < n; i++)
        if (n % i == 0) sum += i;
    return sum == n;
}

int main() {
    int n;
    printf("Enter number: ");
    scanf("%d", &n);
    printf(isPerfect(n) ? "Perfect Number\n" : "Not Perfect\n");
    return 0;
}
```

---

## Day 13

### Q49. Input and display array

**Logic:** Simple array input/output loop.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Array: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

### Q50. Find sum and average of array

**Logic:** Accumulate sum while reading. Divide by n for average.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n]; float sum = 0;
    for (int i = 0; i < n; i++) { scanf("%d", &arr[i]); sum += arr[i]; }
    printf("Sum = %.0f, Average = %.2f\n", sum, sum / n);
    return 0;
}
```

---

### Q51. Find largest and smallest element

**Logic:** Initialize max and min with `arr[0]`, then update by scanning the rest.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    int max = arr[0], min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) max = arr[i];
        if (arr[i] < min) min = arr[i];
    }
    printf("Max = %d, Min = %d\n", max, min);
    return 0;
}
```

---

### Q52. Count even and odd elements

**Logic:** Check each element with `% 2` to determine even or odd.

```c
#include <stdio.h>

int main() {
    int n, even = 0, odd = 0;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
        if (arr[i] % 2 == 0) even++; else odd++;
    }
    printf("Even = %d, Odd = %d\n", even, odd);
    return 0;
}
```

---

## Day 14

### Q53. Linear search

**Logic:** Scan each element sequentially until key is found or end is reached.

```c
#include <stdio.h>

int main() {
    int n, key, pos = -1;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Enter key: ");
    scanf("%d", &key);
    for (int i = 0; i < n; i++) if (arr[i] == key) { pos = i; break; }
    if (pos == -1) printf("Not found\n");
    else printf("Found at index %d\n", pos);
    return 0;
}
```

---

### Q54. Frequency of an element

**Logic:** Scan all elements and count matches (don't break, to find all occurrences).

```c
#include <stdio.h>

int main() {
    int n, key, count = 0;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Enter key: ");
    scanf("%d", &key);
    for (int i = 0; i < n; i++) if (arr[i] == key) count++;
    printf("Frequency = %d\n", count);
    return 0;
}
```

---

### Q55. Second largest element

**Logic:** Track the top two distinct values in one pass.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    int max1 = arr[0], max2 = -2147483648;
    for (int i = 1; i < n; i++) {
        if (arr[i] > max1) { max2 = max1; max1 = arr[i]; }
        else if (arr[i] > max2 && arr[i] != max1) max2 = arr[i];
    }
    printf("Second Largest = %d\n", max2);
    return 0;
}
```

---

### Q56. Find duplicates in array

**Logic:** Compare each element with all subsequent elements. O(n²) approach.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Duplicates: ");
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (arr[i] == arr[j]) { printf("%d ", arr[i]); break; }
    printf("\n");
    return 0;
}
```

---

## Day 15

### Q57. Reverse array

**Logic:** Swap elements from both ends moving inward until they meet.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    for (int i = 0, j = n-1; i < j; i++, j--) { int t = arr[i]; arr[i] = arr[j]; arr[j] = t; }
    printf("Reversed: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

### Q58. Rotate array left

**Logic:** Each left rotation shifts all elements left by 1 and places first element at end.

```c
#include <stdio.h>

int main() {
    int n, k;
    printf("Enter size and rotations: ");
    scanf("%d %d", &n, &k);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    k %= n;
    for (int i = 0; i < k; i++) {
        int t = arr[0];
        for (int j = 0; j < n-1; j++) arr[j] = arr[j+1];
        arr[n-1] = t;
    }
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

### Q59. Rotate array right

**Logic:** Each right rotation shifts all elements right by 1 and places last element at front.

```c
#include <stdio.h>

int main() {
    int n, k;
    printf("Enter size and rotations: ");
    scanf("%d %d", &n, &k);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    k %= n;
    for (int i = 0; i < k; i++) {
        int t = arr[n-1];
        for (int j = n-1; j > 0; j--) arr[j] = arr[j-1];
        arr[0] = t;
    }
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

### Q60. Move zeroes to end

**Logic:** Two-pointer approach: move non-zero elements forward, fill rest with zeros.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    int pos = 0;
    for (int i = 0; i < n; i++) if (arr[i] != 0) arr[pos++] = arr[i];
    while (pos < n) arr[pos++] = 0;
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

## Day 16

### Q61. Find missing number in array

**Logic:** Expected sum of `1 to n+1` minus actual sum gives the missing number.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size (array has 1..n+1 with one missing): ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    int expected = (n + 1) * (n + 2) / 2, actual = 0;
    for (int i = 0; i < n; i++) actual += arr[i];
    printf("Missing = %d\n", expected - actual);
    return 0;
}
```

---

### Q62. Find maximum frequency element

**Logic:** Count frequency of each element; track the one with highest count.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    int maxFreq = 0, elem = arr[0];
    for (int i = 0; i < n; i++) {
        int count = 0;
        for (int j = 0; j < n; j++) if (arr[j] == arr[i]) count++;
        if (count > maxFreq) { maxFreq = count; elem = arr[i]; }
    }
    printf("Max frequency element = %d (freq %d)\n", elem, maxFreq);
    return 0;
}
```

---

### Q63. Find pair with given sum

**Logic:** Check all pairs using nested loops.

```c
#include <stdio.h>

int main() {
    int n, target;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Enter target sum: ");
    scanf("%d", &target);
    for (int i = 0; i < n-1; i++)
        for (int j = i+1; j < n; j++)
            if (arr[i] + arr[j] == target)
                printf("(%d, %d)\n", arr[i], arr[j]);
    return 0;
}
```

---

### Q64. Remove duplicates from array

**Logic:** Build a new result array, adding each element only if not already present.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n], result[n], rsize = 0;
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    for (int i = 0; i < n; i++) {
        int dup = 0;
        for (int j = 0; j < rsize; j++) if (result[j] == arr[i]) { dup = 1; break; }
        if (!dup) result[rsize++] = arr[i];
    }
    printf("After removal: ");
    for (int i = 0; i < rsize; i++) printf("%d ", result[i]);
    printf("\n");
    return 0;
}
```

---

## Day 17

### Q65. Merge arrays

**Logic:** Copy first array into c, then append second array.

```c
#include <stdio.h>

int main() {
    int m, n;
    printf("Enter sizes: ");
    scanf("%d %d", &m, &n);
    int a[m], b[n], c[m+n];
    for (int i = 0; i < m; i++) scanf("%d", &a[i]);
    for (int i = 0; i < n; i++) scanf("%d", &b[i]);
    for (int i = 0; i < m; i++) c[i] = a[i];
    for (int i = 0; i < n; i++) c[m+i] = b[i];
    printf("Merged: ");
    for (int i = 0; i < m+n; i++) printf("%d ", c[i]);
    printf("\n");
    return 0;
}
```

---

### Q66. Union of arrays

**Logic:** Add elements to result only if not already present.

```c
#include <stdio.h>

int inArr(int *a, int size, int val) {
    for (int i = 0; i < size; i++) if (a[i] == val) return 1;
    return 0;
}

int main() {
    int m, n;
    printf("Enter sizes: ");
    scanf("%d %d", &m, &n);
    int a[m], b[n], u[m+n]; int us = 0;
    for (int i = 0; i < m; i++) scanf("%d", &a[i]);
    for (int i = 0; i < n; i++) scanf("%d", &b[i]);
    for (int i = 0; i < m; i++) if (!inArr(u, us, a[i])) u[us++] = a[i];
    for (int i = 0; i < n; i++) if (!inArr(u, us, b[i])) u[us++] = b[i];
    printf("Union: ");
    for (int i = 0; i < us; i++) printf("%d ", u[i]);
    printf("\n");
    return 0;
}
```

---

### Q67. Intersection of arrays

**Logic:** Print elements of array `a` that also exist in array `b`.

```c
#include <stdio.h>

int main() {
    int m, n;
    printf("Enter sizes: ");
    scanf("%d %d", &m, &n);
    int a[m], b[n];
    for (int i = 0; i < m; i++) scanf("%d", &a[i]);
    for (int i = 0; i < n; i++) scanf("%d", &b[i]);
    printf("Intersection: ");
    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            if (a[i] == b[j]) { printf("%d ", a[i]); break; }
    printf("\n");
    return 0;
}
```

---

### Q68. Find common elements

**Logic:** Similar to intersection — prints each element from `a` that appears in `b`.

```c
#include <stdio.h>

int main() {
    int m, n;
    printf("Enter sizes of two arrays: ");
    scanf("%d %d", &m, &n);
    int a[m], b[n];
    for (int i = 0; i < m; i++) scanf("%d", &a[i]);
    for (int i = 0; i < n; i++) scanf("%d", &b[i]);
    printf("Common elements: ");
    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            if (a[i] == b[j]) { printf("%d ", a[i]); break; }
    printf("\n");
    return 0;
}
```

---

## Day 18

### Q69. Bubble sort

**Logic:** Repeatedly swap adjacent elements if out of order. Largest element bubbles to end each pass.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    for (int i = 0; i < n-1; i++)
        for (int j = 0; j < n-i-1; j++)
            if (arr[j] > arr[j+1]) { int t=arr[j]; arr[j]=arr[j+1]; arr[j+1]=t; }
    printf("Sorted: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

### Q70. Selection sort

**Logic:** Find the minimum element in the unsorted portion and place it at the beginning.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    for (int i = 0; i < n-1; i++) {
        int minIdx = i;
        for (int j = i+1; j < n; j++) if (arr[j] < arr[minIdx]) minIdx = j;
        int t = arr[i]; arr[i] = arr[minIdx]; arr[minIdx] = t;
    }
    printf("Sorted: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

### Q71. Binary search

**Logic:** Works only on sorted arrays. Halves the search space each iteration — O(log n).

```c
#include <stdio.h>

int main() {
    int n, key;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    printf("Enter sorted array: ");
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Enter key: ");
    scanf("%d", &key);
    int lo = 0, hi = n-1, mid;
    while (lo <= hi) {
        mid = (lo + hi) / 2;
        if (arr[mid] == key) { printf("Found at index %d\n", mid); return 0; }
        else if (arr[mid] < key) lo = mid + 1;
        else hi = mid - 1;
    }
    printf("Not found\n");
    return 0;
}
```

---

### Q72. Sort array in descending order

**Logic:** Bubble sort variant: swap when left element is smaller than right.

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    for (int i = 0; i < n-1; i++)
        for (int j = 0; j < n-i-1; j++)
            if (arr[j] < arr[j+1]) { int t=arr[j]; arr[j]=arr[j+1]; arr[j+1]=t; }
    printf("Descending: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

## Day 19

### Q73. Add matrices

**Logic:** Add corresponding elements of two matrices of the same size.

```c
#include <stdio.h>

int main() {
    int r, c;
    printf("Enter rows and cols: ");
    scanf("%d %d", &r, &c);
    int a[r][c], b[r][c];
    printf("Matrix A:\n");
    for (int i=0;i<r;i++) for(int j=0;j<c;j++) scanf("%d",&a[i][j]);
    printf("Matrix B:\n");
    for (int i=0;i<r;i++) for(int j=0;j<c;j++) scanf("%d",&b[i][j]);
    printf("Sum:\n");
    for (int i=0;i<r;i++) { for(int j=0;j<c;j++) printf("%d ",a[i][j]+b[i][j]); printf("\n"); }
    return 0;
}
```

---

### Q74. Subtract matrices

**Logic:** Subtract `b[i][j]` from `a[i][j]` element-by-element.

```c
#include <stdio.h>

int main() {
    int r, c;
    printf("Enter rows and cols: ");
    scanf("%d %d", &r, &c);
    int a[r][c], b[r][c];
    for (int i=0;i<r;i++) for(int j=0;j<c;j++) scanf("%d",&a[i][j]);
    for (int i=0;i<r;i++) for(int j=0;j<c;j++) scanf("%d",&b[i][j]);
    printf("Difference:\n");
    for (int i=0;i<r;i++) { for(int j=0;j<c;j++) printf("%d ",a[i][j]-b[i][j]); printf("\n"); }
    return 0;
}
```

---

### Q75. Transpose matrix

**Logic:** Print column `j` of original as row `j` of transpose.

```c
#include <stdio.h>

int main() {
    int r, c;
    printf("Enter rows and cols: ");
    scanf("%d %d", &r, &c);
    int a[r][c];
    for (int i=0;i<r;i++) for(int j=0;j<c;j++) scanf("%d",&a[i][j]);
    printf("Transpose:\n");
    for (int j=0;j<c;j++) { for(int i=0;i<r;i++) printf("%d ",a[i][j]); printf("\n"); }
    return 0;
}
```

---

### Q76. Find diagonal sum

**Logic:** Elements where row index equals column index (`i == j`) form the main diagonal.

```c
#include <stdio.h>

int main() {
    int n, sum = 0;
    printf("Enter matrix size: ");
    scanf("%d", &n);
    int a[n][n];
    for (int i=0;i<n;i++) for(int j=0;j<n;j++) scanf("%d",&a[i][j]);
    for (int i=0;i<n;i++) sum += a[i][i];
    printf("Diagonal sum = %d\n", sum);
    return 0;
}
```

---

## Day 20

### Q77. Multiply matrices

**Logic:** `Result[i][j]` = dot product of row `i` of A and column `j` of B. Requires columns of A = rows of B.

```c
#include <stdio.h>

int main() {
    int r1,c1,r2,c2;
    printf("Enter dimensions (r1 c1 r2 c2): ");
    scanf("%d%d%d%d",&r1,&c1,&r2,&c2);
    if(c1!=r2){printf("Incompatible!\n");return 1;}
    int a[r1][c1],b[r2][c2],res[r1][c2];
    for(int i=0;i<r1;i++) for(int j=0;j<c1;j++) scanf("%d",&a[i][j]);
    for(int i=0;i<r2;i++) for(int j=0;j<c2;j++) scanf("%d",&b[i][j]);
    for(int i=0;i<r1;i++) for(int j=0;j<c2;j++) {
        res[i][j]=0;
        for(int k=0;k<c1;k++) res[i][j]+=a[i][k]*b[k][j];
    }
    for(int i=0;i<r1;i++){for(int j=0;j<c2;j++) printf("%d ",res[i][j]);printf("\n");}
    return 0;
}
```

---

### Q78. Check symmetric matrix

**Logic:** A matrix is symmetric if `A[i][j] == A[j][i]` for all i, j.

```c
#include <stdio.h>

int main() {
    int n, sym = 1;
    printf("Enter size: ");
    scanf("%d",&n);
    int a[n][n];
    for(int i=0;i<n;i++) for(int j=0;j<n;j++) scanf("%d",&a[i][j]);
    for(int i=0;i<n&&sym;i++) for(int j=0;j<n&&sym;j++) if(a[i][j]!=a[j][i]) sym=0;
    printf(sym?"Symmetric\n":"Not Symmetric\n");
    return 0;
}
```

---

### Q79. Find row-wise sum

**Logic:** Sum elements in each row individually.

```c
#include <stdio.h>

int main() {
    int r,c;
    printf("Enter rows cols: ");
    scanf("%d%d",&r,&c);
    int a[r][c];
    for(int i=0;i<r;i++) for(int j=0;j<c;j++) scanf("%d",&a[i][j]);
    for(int i=0;i<r;i++){
        int s=0;
        for(int j=0;j<c;j++) s+=a[i][j];
        printf("Row %d sum = %d\n",i+1,s);
    }
    return 0;
}
```

---

### Q80. Find column-wise sum

**Logic:** Sum elements in each column individually.

```c
#include <stdio.h>

int main() {
    int r,c;
    printf("Enter rows cols: ");
    scanf("%d%d",&r,&c);
    int a[r][c];
    for(int i=0;i<r;i++) for(int j=0;j<c;j++) scanf("%d",&a[i][j]);
    for(int j=0;j<c;j++){
        int s=0;
        for(int i=0;i<r;i++) s+=a[i][j];
        printf("Col %d sum = %d\n",j+1,s);
    }
    return 0;
}
```

---

## Day 21

### Q81. Find string length without strlen()

**Logic:** Count characters until null terminator `'\0'` is reached.

```c
#include <stdio.h>

int main() {
    char s[100];
    printf("Enter string: ");
    scanf("%s", s);
    int len = 0;
    while (s[len] != '\0') len++;
    printf("Length = %d\n", len);
    return 0;
}
```

---

### Q82. Reverse a string

**Logic:** Two-pointer swap from both ends moving inward.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char s[100];
    printf("Enter string: ");
    scanf("%s", s);
    int n = strlen(s);
    for (int i=0,j=n-1; i<j; i++,j--) { char t=s[i]; s[i]=s[j]; s[j]=t; }
    printf("Reversed: %s\n", s);
    return 0;
}
```

---

### Q83. Count vowels and consonants

**Logic:** Convert to lowercase, check if letter, then check if it's a vowel.

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char s[100]; int v=0,c=0;
    printf("Enter string: ");
    gets(s);
    for (int i=0; s[i]; i++) {
        char ch = tolower(s[i]);
        if (isalpha(ch)) {
            if (ch=='a'||ch=='e'||ch=='i'||ch=='o'||ch=='u') v++;
            else c++;
        }
    }
    printf("Vowels=%d, Consonants=%d\n",v,c);
    return 0;
}
```

---

### Q84. Convert lowercase to uppercase

**Logic:** Subtract 32 from ASCII value of lowercase letters to get uppercase (or use `toupper()`).

```c
#include <stdio.h>

int main() {
    char s[100];
    printf("Enter string: ");
    gets(s);
    for (int i=0; s[i]; i++)
        if (s[i]>='a' && s[i]<='z') s[i] -= 32;
    printf("%s\n", s);
    return 0;
}
```

---

## Day 22

### Q85. Check palindrome string

**Logic:** Compare character at position `i` with character at position `(n-1-i)`.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char s[100];
    printf("Enter string: ");
    scanf("%s",s);
    int n=strlen(s),pal=1;
    for(int i=0;i<n/2;i++) if(s[i]!=s[n-i-1]){pal=0;break;}
    printf(pal?"Palindrome\n":"Not Palindrome\n");
    return 0;
}
```

---

### Q86. Count words in a sentence

**Logic:** Track when a new word starts (non-space after space or at start).

```c
#include <stdio.h>

int main() {
    char s[200]; int count=0,inWord=0;
    printf("Enter sentence: ");
    gets(s);
    for(int i=0;s[i];i++){
        if(s[i]!=' '&&!inWord){count++;inWord=1;}
        else if(s[i]==' ') inWord=0;
    }
    printf("Words = %d\n",count);
    return 0;
}
```

---

### Q87. Character frequency

**Logic:** Count occurrences of a specific character in the string.

```c
#include <stdio.h>

int main() {
    char s[200], ch;
    int count=0;
    printf("Enter string: "); gets(s);
    printf("Enter character: "); scanf("%c",&ch);
    for(int i=0;s[i];i++) if(s[i]==ch) count++;
    printf("Frequency of '%c' = %d\n",ch,count);
    return 0;
}
```

---

### Q88. Remove spaces from string

**Logic:** Copy non-space characters to same array starting from index 0.

```c
#include <stdio.h>

int main() {
    char s[200]; int k=0;
    printf("Enter string: "); gets(s);
    for(int i=0;s[i];i++) if(s[i]!=' ') s[k++]=s[i];
    s[k]='\0';
    printf("%s\n",s);
    return 0;
}
```

---

## Day 23

### Q89. Find first non-repeating character

**Logic:** Count frequency of all characters, then find the first one with frequency 1.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char s[100]; int freq[256]={0};
    printf("Enter string: "); scanf("%s",s);
    for(int i=0;s[i];i++) freq[(int)s[i]]++;
    for(int i=0;s[i];i++) if(freq[(int)s[i]]==1){printf("First non-repeating: %c\n",s[i]);return 0;}
    printf("None\n"); return 0;
}
```

---

### Q90. Find first repeating character

**Logic:** Count frequency of all characters, then find the first one with frequency > 1.

```c
#include <stdio.h>

int main() {
    char s[100]; int freq[256]={0};
    printf("Enter string: "); scanf("%s",s);
    for(int i=0;s[i];i++) freq[(int)s[i]]++;
    for(int i=0;s[i];i++) if(freq[(int)s[i]]>1){printf("First repeating: %c\n",s[i]);return 0;}
    printf("None\n"); return 0;
}
```

---

### Q91. Check anagram strings

**Logic:** Two strings are anagrams if they have the same character frequencies.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char a[100],b[100]; int fa[256]={0},fb[256]={0};
    printf("Enter two strings: "); scanf("%s%s",a,b);
    for(int i=0;a[i];i++) fa[(int)a[i]]++;
    for(int i=0;b[i];i++) fb[(int)b[i]]++;
    int anagram=1;
    for(int i=0;i<256;i++) if(fa[i]!=fb[i]){anagram=0;break;}
    printf(anagram?"Anagram\n":"Not Anagram\n");
    return 0;
}
```

---

### Q92. Find maximum occurring character

**Logic:** Track character with highest frequency in a 256-element frequency array.

```c
#include <stdio.h>

int main() {
    char s[100]; int freq[256]={0};
    printf("Enter string: "); scanf("%s",s);
    for(int i=0;s[i];i++) freq[(int)s[i]]++;
    int maxF=0,maxC='a';
    for(int i=0;i<256;i++) if(freq[i]>maxF){maxF=freq[i];maxC=i;}
    printf("Max char: %c (freq %d)\n",(char)maxC,maxF);
    return 0;
}
```

---

## Day 24

### Q93. Check string rotation

**Logic:** If `b` is a rotation of `a`, then `b` will appear as a substring of `a+a`.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char a[100],b[200];
    printf("Enter two strings: "); scanf("%s",a);
    char temp[200]; strcpy(temp,a); strcat(temp,a);
    scanf("%s",b);
    printf(strstr(temp,b)?"Is rotation\n":"Not rotation\n");
    return 0;
}
```

---

### Q94. Compress a string

**Logic:** Run-length encoding: replace consecutive same characters with char+count.

```c
#include <stdio.h>

int main() {
    char s[100]; int i=0;
    printf("Enter string: "); scanf("%s",s);
    while(s[i]){
        char ch=s[i]; int count=0;
        while(s[i]==ch){count++;i++;}
        printf("%c%d",ch,count);
    }
    printf("\n");
    return 0;
}
```

---

### Q95. Find longest word

**Logic:** Extract words by splitting on spaces and track the one with maximum length.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char s[200],word[50],longest[50]=""; int maxLen=0;
    printf("Enter sentence: "); gets(s);
    int i=0;
    while(s[i]){
        int j=0;
        while(s[i]&&s[i]!=' ') word[j++]=s[i++];
        word[j]='\0';
        if(j>maxLen){maxLen=j;strcpy(longest,word);}
        if(s[i]) i++;
    }
    printf("Longest word: %s\n",longest);
    return 0;
}
```

---

### Q96. Remove duplicate characters

**Logic:** Keep a boolean array to track which characters have been seen.

```c
#include <stdio.h>

int main() {
    char s[100]; int seen[256]={0}; int k=0;
    printf("Enter string: "); scanf("%s",s);
    for(int i=0;s[i];i++) if(!seen[(int)s[i]]){s[k++]=s[i];seen[(int)s[i]]=1;}
    s[k]='\0';
    printf("%s\n",s);
    return 0;
}
```

---

## Day 25

### Q97. Merge two sorted arrays

**Logic:** Two-pointer merge: compare front elements of both arrays and pick the smaller.

```c
#include <stdio.h>

int main() {
    int m,n;
    printf("Enter sizes: "); scanf("%d%d",&m,&n);
    int a[m],b[n],c[m+n];
    for(int i=0;i<m;i++) scanf("%d",&a[i]);
    for(int i=0;i<n;i++) scanf("%d",&b[i]);
    int i=0,j=0,k=0;
    while(i<m&&j<n) c[k++]=(a[i]<b[j])?a[i++]:b[j++];
    while(i<m) c[k++]=a[i++];
    while(j<n) c[k++]=b[j++];
    for(int i=0;i<m+n;i++) printf("%d ",c[i]);
    printf("\n");
    return 0;
}
```

---

### Q98. Find common characters in strings

**Logic:** Mark characters present in each string using boolean arrays, then find overlap.

```c
#include <stdio.h>

int main() {
    char a[100],b[100]; int fa[256]={0},fb[256]={0};
    printf("Enter two strings: "); scanf("%s%s",a,b);
    for(int i=0;a[i];i++) fa[(int)a[i]]=1;
    for(int i=0;b[i];i++) fb[(int)b[i]]=1;
    printf("Common: ");
    for(int i=32;i<127;i++) if(fa[i]&&fb[i]) printf("%c ",(char)i);
    printf("\n");
    return 0;
}
```

---

### Q99. Sort names alphabetically

**Logic:** Bubble sort using `strcmp()` to compare strings lexicographically.

```c
#include <stdio.h>
#include <string.h>

int main() {
    int n; printf("Enter count: "); scanf("%d",&n);
    char names[n][50], temp[50];
    for(int i=0;i<n;i++) scanf("%s",names[i]);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)
            if(strcmp(names[j],names[j+1])>0){strcpy(temp,names[j]);strcpy(names[j],names[j+1]);strcpy(names[j+1],temp);}
    for(int i=0;i<n;i++) printf("%s\n",names[i]);
    return 0;
}
```

---

### Q100. Sort words by length

**Logic:** Bubble sort using `strlen()` for comparison instead of `strcmp()`.

```c
#include <stdio.h>
#include <string.h>

int main() {
    int n; printf("Enter count: "); scanf("%d",&n);
    char words[n][50], temp[50];
    for(int i=0;i<n;i++) scanf("%s",words[i]);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)
            if(strlen(words[j])>strlen(words[j+1])){strcpy(temp,words[j]);strcpy(words[j],words[j+1]);strcpy(words[j+1],temp);}
    for(int i=0;i<n;i++) printf("%s\n",words[i]);
    return 0;
}
```

---

## Day 26

### Q101. Number guessing game

**Logic:** Generate a random number, then give higher/lower hints until the user guesses correctly.

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    srand(time(0));
    int secret = rand() % 100 + 1, guess, attempts = 0;
    printf("Guess a number between 1 and 100:\n");
    do {
        scanf("%d",&guess); attempts++;
        if(guess<secret) printf("Too low!\n");
        else if(guess>secret) printf("Too high!\n");
        else printf("Correct! Attempts: %d\n",attempts);
    } while(guess!=secret);
    return 0;
}
```

---

### Q102. Voting eligibility system

**Logic:** Simple age check: eligible if `age >= 18`.

```c
#include <stdio.h>

int main() {
    int age;
    printf("Enter your age: ");
    scanf("%d",&age);
    printf(age>=18?"Eligible to vote\n":"Not eligible to vote\n");
    return 0;
}
```

---

### Q103. ATM simulation

**Logic:** Menu-driven loop for balance check, deposit, and withdrawal with validation.

```c
#include <stdio.h>

int main() {
    float balance=5000; int choice; float amount;
    while(1){
        printf("\n1.Check Balance 2.Deposit 3.Withdraw 4.Exit\nChoice: ");
        scanf("%d",&choice);
        if(choice==1) printf("Balance: %.2f\n",balance);
        else if(choice==2){printf("Amount: ");scanf("%f",&amount);balance+=amount;printf("Deposited\n");}
        else if(choice==3){printf("Amount: ");scanf("%f",&amount);if(amount>balance)printf("Insufficient!\n");else{balance-=amount;printf("Withdrawn\n");}}
        else break;
    }
    return 0;
}
```

---

### Q104. Quiz application

**Logic:** Array of questions and answers; compare user input with stored answer using `strcmp`.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char *qs[]={"Capital of India?","2+2=?","C extension?"};
    char *ans[]={"delhi","4",".c"};
    int score=0; char input[50];
    for(int i=0;i<3;i++){
        printf("Q%d: %s\nAnswer: ",i+1,qs[i]);
        scanf("%s",input);
        if(strcmp(input,ans[i])==0){printf("Correct!\n");score++;}
        else printf("Wrong! Answer: %s\n",ans[i]);
    }
    printf("Score: %d/3\n",score);
    return 0;
}
```

---

## Day 27

### Q105. Student record management system

**Logic:** Use a struct to hold student data. Input and display in tabular form.

```c
#include <stdio.h>
#include <string.h>

struct Student { char name[50]; int roll; float marks; };

int main() {
    int n; printf("Enter students: "); scanf("%d",&n);
    struct Student s[n];
    for(int i=0;i<n;i++){
        printf("Name, Roll, Marks: ");
        scanf("%s%d%f",s[i].name,&s[i].roll,&s[i].marks);
    }
    printf("\n%-15s%-10s%-10s\n","Name","Roll","Marks");
    for(int i=0;i<n;i++) printf("%-15s%-10d%-10.2f\n",s[i].name,s[i].roll,s[i].marks);
    return 0;
}
```

---

### Q106. Employee management system

**Logic:** Similar to student records using an Employee struct.

```c
#include <stdio.h>

struct Employee { char name[50]; int id; float salary; };

int main() {
    int n; printf("Enter employees: "); scanf("%d",&n);
    struct Employee e[n];
    for(int i=0;i<n;i++){
        printf("Name, ID, Salary: ");
        scanf("%s%d%f",e[i].name,&e[i].id,&e[i].salary);
    }
    printf("\n%-15s%-10s%-10s\n","Name","ID","Salary");
    for(int i=0;i<n;i++) printf("%-15s%-10d%-10.2f\n",e[i].name,e[i].id,e[i].salary);
    return 0;
}
```

---

### Q107. Salary management system

**Logic:** Calculate HRA (20%), DA (50%), gross, deductions (10%), and net salary.

```c
#include <stdio.h>

int main() {
    float basic, hra, da, gross, deductions, net;
    printf("Enter basic salary: "); scanf("%f",&basic);
    hra = 0.20 * basic;
    da  = 0.50 * basic;
    gross = basic + hra + da;
    deductions = 0.10 * basic;
    net = gross - deductions;
    printf("HRA=%.2f DA=%.2f Gross=%.2f Net=%.2f\n",hra,da,gross,net);
    return 0;
}
```

---

### Q108. Marksheet generation system

**Logic:** Collect marks for n subjects and compute total, average, percentage and grade.

```c
#include <stdio.h>

int main() {
    char name[50]; int roll,n; float total=0,marks;
    printf("Name, Roll, Subjects: "); scanf("%s%d%d",name,&roll,&n);
    for(int i=0;i<n;i++){printf("Subject %d marks: ",i+1);scanf("%f",&marks);total+=marks;}
    float avg=total/n, percent=(total/(n*100))*100;
    char *grade = avg>=90?"A+":avg>=75?"A":avg>=60?"B":avg>=50?"C":"F";
    printf("\nMarksheet\nName: %s Roll: %d\nTotal: %.0f Avg: %.2f Percent: %.2f%% Grade: %s\n",name,roll,total,avg,percent,grade);
    return 0;
}
```

---

## Day 28

### Q109. Library management system

**Logic:** Supports adding, displaying, issuing, and returning books using a struct array.

```c
#include <stdio.h>
#include <string.h>

struct Book { char title[50]; char author[50]; int avail; };

int main() {
    struct Book books[5]; int n=0,choice;
    while(1){
        printf("1.Add 2.Display 3.Issue 4.Return 5.Exit: ");
        scanf("%d",&choice);
        if(choice==1){printf("Title Author: ");scanf("%s%s",books[n].title,books[n].author);books[n].avail=1;n++;}
        else if(choice==2){for(int i=0;i<n;i++) printf("%s by %s [%s]\n",books[i].title,books[i].author,books[i].avail?"Available":"Issued");}
        else if(choice==3){char t[50];printf("Title: ");scanf("%s",t);for(int i=0;i<n;i++) if(strcmp(books[i].title,t)==0) books[i].avail=0;}
        else if(choice==4){char t[50];printf("Title: ");scanf("%s",t);for(int i=0;i<n;i++) if(strcmp(books[i].title,t)==0) books[i].avail=1;}
        else break;
    }
    return 0;
}
```

---

### Q110. Bank account system

**Logic:** Struct-based bank account with deposit, withdrawal, and balance inquiry.

```c
#include <stdio.h>

struct Account { char owner[50]; int accNo; float balance; };

int main() {
    struct Account acc; int choice; float amt;
    printf("Name, Account No, Initial Balance: ");
    scanf("%s%d%f",acc.owner,&acc.accNo,&acc.balance);
    while(1){
        printf("1.Deposit 2.Withdraw 3.Balance 4.Exit: ");
        scanf("%d",&choice);
        if(choice==1){printf("Amount: ");scanf("%f",&amt);acc.balance+=amt;printf("Deposited\n");}
        else if(choice==2){printf("Amount: ");scanf("%f",&amt);if(amt>acc.balance)printf("Insufficient\n");else{acc.balance-=amt;printf("Withdrawn\n");}}
        else if(choice==3) printf("Balance: %.2f\n",acc.balance);
        else break;
    }
    return 0;
}
```

---

### Q111. Ticket booking system

**Logic:** Array of 10 seats; 0 = free, 1 = booked. Menu-driven booking and cancellation.

```c
#include <stdio.h>

int seats[10]={0};

int main() {
    int choice,seatNo;
    while(1){
        printf("1.Book 2.Cancel 3.View 4.Exit: ");
        scanf("%d",&choice);
        if(choice==1){printf("Seat (1-10): ");scanf("%d",&seatNo);if(seats[seatNo-1])printf("Already Booked!\n");else{seats[seatNo-1]=1;printf("Booking done\n");}}
        else if(choice==2){printf("Seat (1-10): ");scanf("%d",&seatNo);if(!seats[seatNo-1])printf("Not booked\n");else{seats[seatNo-1]=0;printf("Cancelled\n");}}
        else if(choice==3){for(int i=0;i<10;i++) printf("Seat %d: %s\n",i+1,seats[i]?"Booked":"Free");}
        else break;
    }
    return 0;
}
```

---

### Q112. Contact management system

**Logic:** Add, search by name, and display all contacts using a struct array.

```c
#include <stdio.h>
#include <string.h>

struct Contact { char name[50]; char phone[15]; };
struct Contact contacts[100]; int n=0;

int main() {
    int choice;
    while(1){
        printf("1.Add 2.Search 3.Display 4.Exit: "); scanf("%d",&choice);
        if(choice==1){printf("Name Phone: ");scanf("%s%s",contacts[n].name,contacts[n].phone);n++;}
        else if(choice==2){char nm[50];printf("Name: ");scanf("%s",nm);for(int i=0;i<n;i++) if(strcmp(contacts[i].name,nm)==0) printf("%s: %s\n",contacts[i].name,contacts[i].phone);}
        else if(choice==3){for(int i=0;i<n;i++) printf("%s: %s\n",contacts[i].name,contacts[i].phone);}
        else break;
    }
    return 0;
}
```

---

## Day 29

### Q113. Menu-driven calculator

**Logic:** Simple menu loop supporting add, subtract, multiply, divide with division-by-zero guard.

```c
#include <stdio.h>

int main() {
    float a,b; int choice;
    printf("Enter two numbers: "); scanf("%f%f",&a,&b);
    while(1){
        printf("1.Add 2.Sub 3.Mul 4.Div 5.Exit: "); scanf("%d",&choice);
        if(choice==1) printf("%.2f\n",a+b);
        else if(choice==2) printf("%.2f\n",a-b);
        else if(choice==3) printf("%.2f\n",a*b);
        else if(choice==4){if(b==0)printf("Error: Division by zero\n");else printf("%.2f\n",a/b);}
        else break;
    }
    return 0;
}
```

---

### Q114. Menu-driven array operations system

**Logic:** Supports dynamic insert, delete, search, display, and sort on a global array.

```c
#include <stdio.h>

int arr[100],n=0;

int main() {
    int choice,val;
    while(1){
        printf("1.Insert 2.Delete 3.Search 4.Display 5.Sort 6.Exit: "); scanf("%d",&choice);
        if(choice==1){printf("Value: ");scanf("%d",&val);arr[n++]=val;}
        else if(choice==2){printf("Value: ");scanf("%d",&val);for(int i=0;i<n;i++) if(arr[i]==val){for(int j=i;j<n-1;j++) arr[j]=arr[j+1];n--;break;}}
        else if(choice==3){printf("Value: ");scanf("%d",&val);int f=0;for(int i=0;i<n;i++) if(arr[i]==val){printf("Found at %d\n",i);f=1;}if(!f)printf("Not found\n");}
        else if(choice==4){for(int i=0;i<n;i++) printf("%d ",arr[i]);printf("\n");}
        else if(choice==5){for(int i=0;i<n-1;i++) for(int j=0;j<n-i-1;j++) if(arr[j]>arr[j+1]){int t=arr[j];arr[j]=arr[j+1];arr[j+1]=t;}}
        else break;
    }
    return 0;
}
```

---

### Q115. Menu-driven string operations system

**Logic:** Menu for common string operations: length, reverse, uppercase, lowercase, palindrome check.

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char s[200]; int choice;
    printf("Enter string: "); gets(s);
    while(1){
        printf("1.Length 2.Reverse 3.Upper 4.Lower 5.Palindrome 6.Exit: "); scanf("%d",&choice);
        if(choice==1) printf("Length: %lu\n",strlen(s));
        else if(choice==2){int n=strlen(s);for(int i=0,j=n-1;i<j;i++,j--){char t=s[i];s[i]=s[j];s[j]=t;}printf("%s\n",s);}
        else if(choice==3){char tmp[200];strcpy(tmp,s);for(int i=0;tmp[i];i++) tmp[i]=toupper(tmp[i]);printf("%s\n",tmp);}
        else if(choice==4){char tmp[200];strcpy(tmp,s);for(int i=0;tmp[i];i++) tmp[i]=tolower(tmp[i]);printf("%s\n",tmp);}
        else if(choice==5){int n=strlen(s),pal=1;for(int i=0;i<n/2;i++) if(s[i]!=s[n-i-1]){pal=0;break;}printf(pal?"Palindrome\n":"Not Palindrome\n");}
        else break;
    }
    return 0;
}
```

---

### Q116. Inventory management system

**Logic:** Struct-based inventory with add, display, update, and search by name.

```c
#include <stdio.h>
#include <string.h>

struct Item { char name[50]; int qty; float price; };
struct Item inv[100]; int n=0;

int main() {
    int choice;
    while(1){
        printf("1.Add 2.Display 3.Update 4.Search 5.Exit: "); scanf("%d",&choice);
        if(choice==1){printf("Name Qty Price: ");scanf("%s%d%f",inv[n].name,&inv[n].qty,&inv[n].price);n++;}
        else if(choice==2){printf("%-15s%-10s%-10s\n","Name","Qty","Price");for(int i=0;i<n;i++) printf("%-15s%-10d%-10.2f\n",inv[i].name,inv[i].qty,inv[i].price);}
        else if(choice==3){char nm[50];printf("Name: ");scanf("%s",nm);for(int i=0;i<n;i++) if(strcmp(inv[i].name,nm)==0){printf("New Qty Price: ");scanf("%d%f",&inv[i].qty,&inv[i].price);}}
        else if(choice==4){char nm[50];printf("Name: ");scanf("%s",nm);for(int i=0;i<n;i++) if(strcmp(inv[i].name,nm)==0) printf("Found: Qty=%d Price=%.2f\n",inv[i].qty,inv[i].price);}
        else break;
    }
    return 0;
}
```

---

## Day 30

### Q117. Student record system using arrays and strings

**Logic:** 2D array for marks (students × subjects). Calculate totals and averages.

```c
#include <stdio.h>

int main() {
    int n; printf("Enter students: "); scanf("%d",&n);
    char names[n][50]; int roll[n]; float marks[n][5],total[n];
    for(int i=0;i<n;i++){
        printf("Name Roll: "); scanf("%s%d",names[i],&roll[i]);
        total[i]=0;
        for(int j=0;j<5;j++){printf("Subject %d: ",j+1);scanf("%f",&marks[i][j]);total[i]+=marks[i][j];}
    }
    printf("\n%-15s%-8s%-10s%-8s\n","Name","Roll","Total","Avg");
    for(int i=0;i<n;i++) printf("%-15s%-8d%-10.1f%-8.1f\n",names[i],roll[i],total[i],total[i]/5);
    return 0;
}
```

---

### Q118. Mini library system

**Logic:** Library system using parallel arrays for title, author, and availability status.

```c
#include <stdio.h>
#include <string.h>

char titles[20][50],authors[20][50]; int avail[20]; int nb=0;

int main() {
    int choice;
    while(1){
        printf("1.Add 2.Issue 3.Return 4.Display 5.Exit: "); scanf("%d",&choice);
        if(choice==1){printf("Title Author: ");scanf("%s%s",titles[nb],authors[nb]);avail[nb]=1;nb++;}
        else if(choice==2){char t[50];printf("Title: ");scanf("%s",t);for(int i=0;i<nb;i++) if(strcmp(titles[i],t)==0&&avail[i]){avail[i]=0;printf("Issued\n");break;}}
        else if(choice==3){char t[50];printf("Title: ");scanf("%s",t);for(int i=0;i<nb;i++) if(strcmp(titles[i],t)==0&&!avail[i]){avail[i]=1;printf("Returned\n");break;}}
        else if(choice==4){for(int i=0;i<nb;i++) printf("%s by %s [%s]\n",titles[i],authors[i],avail[i]?"Available":"Issued");}
        else break;
    }
    return 0;
}
```

---

### Q119. Mini employee management system

**Logic:** Parallel arrays for employee data with CRUD: add, display, search by ID, delete by ID.

```c
#include <stdio.h>
#include <string.h>

char enames[50][50]; int eids[50]; float esalary[50]; int ne=0;

int main() {
    int choice;
    while(1){
        printf("1.Add 2.Display 3.Search 4.Delete 5.Exit: "); scanf("%d",&choice);
        if(choice==1){printf("Name ID Salary: ");scanf("%s%d%f",enames[ne],&eids[ne],&esalary[ne]);ne++;}
        else if(choice==2){for(int i=0;i<ne;i++) printf("%s ID=%d Salary=%.2f\n",enames[i],eids[i],esalary[i]);}
        else if(choice==3){int id;printf("ID: ");scanf("%d",&id);for(int i=0;i<ne;i++) if(eids[i]==id) printf("%s %.2f\n",enames[i],esalary[i]);}
        else if(choice==4){int id;printf("ID: ");scanf("%d",&id);for(int i=0;i<ne;i++) if(eids[i]==id){for(int j=i;j<ne-1;j++){strcpy(enames[j],enames[j+1]);eids[j]=eids[j+1];esalary[j]=esalary[j+1];}ne--;break;}}
        else break;
    }
    return 0;
}
```

---

### Q120. Complete mini project – Inventory Management System

**Logic:** Full mini project with modular functions for add, display, search, update quantity, and calculate total inventory value.

```c
#include <stdio.h>
#include <string.h>

#define MAX 50

char pnames[MAX][50]; float prices[MAX]; int quantities[MAX]; int np=0;

void addProduct(){
    if(np>=MAX){printf("Full!\n");return;}
    printf("Name Price Qty: ");
    scanf("%s%f%d",pnames[np],&prices[np],&quantities[np]);
    np++;
    printf("Added.\n");
}

void displayAll(){
    printf("\n%-15s%-12s%-10s\n","Product","Price","Qty");
    for(int i=0;i<np;i++)
        printf("%-15s%-12.2f%-10d\n",pnames[i],prices[i],quantities[i]);
}

void searchProduct(){
    char nm[50]; printf("Name: "); scanf("%s",nm);
    for(int i=0;i<np;i++)
        if(strcmp(pnames[i],nm)==0){
            printf("Found: Price=%.2f Qty=%d\n",prices[i],quantities[i]);
            return;
        }
    printf("Not found.\n");
}

void updateQty(){
    char nm[50]; int q;
    printf("Name NewQty: "); scanf("%s%d",nm,&q);
    for(int i=0;i<np;i++)
        if(strcmp(pnames[i],nm)==0){quantities[i]=q;printf("Updated.\n");return;}
    printf("Not found.\n");
}

void totalValue(){
    float total=0;
    for(int i=0;i<np;i++) total+=prices[i]*quantities[i];
    printf("Total inventory value: %.2f\n",total);
}

int main(){
    int choice;
    printf("=== Mini Inventory Management ===\n");
    while(1){
        printf("\n1.Add 2.Display 3.Search 4.UpdateQty 5.TotalValue 6.Exit: ");
        scanf("%d",&choice);
        if(choice==1) addProduct();
        else if(choice==2) displayAll();
        else if(choice==3) searchProduct();
        else if(choice==4) updateQty();
        else if(choice==5) totalValue();
        else { printf("Goodbye!\n"); break; }
    }
    return 0;
}
```