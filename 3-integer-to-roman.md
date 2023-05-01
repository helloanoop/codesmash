# Integer to Roman

### Metadata

Source: [Leetcode](https://leetcode.com/problems/integer-to-roman) `Medium` <br/>
Solved on: `1 May 2023`


### Problem
Convert integer to roman numeral.

### Constraints

* 0 <= Num <= 3999

### Solution
```javascript
var intToRoman = function(num) {
    var getRomanNumeral = function(number, first, fifth, tenth) {
        var pos = {
            0: '',
            1: first,
            2: `${first}${first}`,
            3: `${first}${first}${first}`,
            4: `${first}${fifth}`,
            5: `${fifth}`,
            6: `${fifth}${first}`,
            7: `${fifth}${first}${first}`,
            8: `${fifth}${first}${first}${first}`,
            9: `${first}${tenth}`
        };
        return pos[parseInt(number)];
    };

    if(!num) return '';

    if(isNaN(num) || num < 0 || num > 3999) throw new Error(`intToRoman: unable to convert the given number: ${num}`);

    if(num < 10) {
        return getRomanNumeral(num % 10, 'I', 'V', 'X');
    }

    if(num < 100) {
        var unit = getRomanNumeral(num % 10, 'I', 'V', 'X')
        var tenth = getRomanNumeral(num / 10, 'X', 'L', 'C');

        return tenth + unit;
    }

    if(num < 1000) {
        var unit = getRomanNumeral(num % 10, 'I', 'V', 'X')
        var tenth = getRomanNumeral((num % 100)/ 10, 'X', 'L', 'C');
        var hundredth = getRomanNumeral(num / 100, '**C**', 'D', 'M');

        return hundredth + tenth + unit;
    }

    if(num <= 3999) {
        var unit = getRomanNumeral(num % 10, 'I', 'V', 'X')
        var tenth =**** getRomanNumeral((num % 100) / **10**, 'X', 'L', 'C');
        var hundredth = getRomanNumeral((num % 1000) / 100, 'C', 'D', 'M');
        var thousandth = getRomanNumeral(num / 1000, 'M');

        return thousandth + hundredth + tenth + unit;
    }
};
```

### Notes
Solved it in 35min. It did take multiple runs to iron edge cases and bugs. And chatgpt whooped my ass.

### ChatGPT
```javascript
var intToRoman = function(num) {
    const romanNumerals = {
        M: 1000,
        CM: 900,
        D: 500,
        CD: 400,
        C: 100,
        XC: 90,
        L: 50,
        XL: 40,
        X: 10,
        IX: 9,
        V: 5,
        IV: 4,
        I: 1,
    };
    let result = '';
    for (const key in romanNumerals) {
        const value = romanNumerals[key];
        while (num >= value) {
            result += key;
            num -= value;
        }
    }
    return result;
};
```



