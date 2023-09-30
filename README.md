[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=11924426&assignment_repo_type=AssignmentRepo)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```
Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

## Answer
The recurrence relation is : T(n) = $3$ * T($\frac{n}{3}$) + $n^5$

T(n) = 2T($\frac{n}{3}$) + $n^2$ * n * $n^2$ + T($\frac{n}{3}$)

T(n) = 3T($\frac{n}{3}$) + $n^5$                                                                                    ---1

T(n) = 3( 3T($\frac{n}{9}$) + $\left(\frac{n}{3}\right)^5$ ) + $n^5$

T(n) = 9T($\frac{n}{9}$) + $\left(\frac{3n^5}{3^5}\right)$ + $n^5$                                                   ---2

T(n) = 3( 9T($\frac{n}{27}$) + ($3\left(\frac{n}{3})^5/{3^5}\right)$ + $\left(\frac{n}{3}\right)^5$) + $n^5$

T(n) = 27T($\frac{n}{27}$) + $\left(\frac{9n^5}{9^5}\right)$ + $\left(\frac{3n^5}{3^5}\right)$ + $n^5$                ---3

T(n) = 81T($\frac{n}{81}$) + 3($9\left(\frac{n}{3})^5/{9^5}\right)$ + 3($3\left(\frac{n}{3})^5/{3^5}\right)$ + $\left(\frac{3n^5}{3^5}\right)$ + $n^5$

T(n) = 81T($\frac{n}{81}$) + $27\left(\frac{n^5}{27^5}\right)$ + $9\left(\frac{n^5}{9^5}\right)$ + $\left(\frac{3n^5}{3^5}\right)$ + $n^5$        ---4

...

T(n) = $3^i$ * T($\frac{n}{3^i}$) + $\displaystyle\sum_{j=0}^{i-1} \frac{3^j}{3^{{j^5}}}$ $n^5$

i = $\log_{3} n$

= $3^{log_{3}n}$ T($\frac{n}{3^{log_{3}n}}$) + $\displaystyle\sum_{j=0}^{3^{log_{3}n}-1} \frac{3^j}{3^{5j}}$ $n^5$

= n + $\log_{3} n$ * $n^5$ $\in \Theta(n^5(log_{3}n))$

