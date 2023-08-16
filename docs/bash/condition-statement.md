# Introduction to conditional statement (If)

Sometimes, you need to take different action depending on the success or failure of a command. 
The ***if*** statement helps you in such conditions.

### Syntax
```
if [ condition ]
then 
    statements 1
    statements 2
    .
    .
    statements n
fi
```
```
if [[ condition ]]
then 
    statements 1
    statements 2
    .
    .
    statements n
fi
```
The **condition** is true or returns 0 (zero), the statements get executed.

#### NOTE:
1. There should be a space with in square brackets at starting and ending.
![space](../assets/space.jpg)
*Picture courtesy: https://kodekloud.com/*

    **Example** 
    ````   
            if [[ 5 -gt 0 ]]
     ````

2. The condition often involves numerical or string comparison tests.
3. The condition returns a status of zero when it succeeds and some other status when it fails.
4. The condition may be a command (e.g ```if [ $(whoami) = "root" ]```)
5. Unary expressions are often used to examine the status of a file