#### 1. What’s the output of this code?
```php
class Foo{
    public function makeFoo(callable $bar) :string {
        return "Hello ".$bar();
    }
}
class Bar{
    public function makeFooBar() :string {
        return (new Foo)->makeFoo([$this, 'makeBar']);
    }
    private function makeBar() :string {
        return "World";
    }
}
echo (new Bar)->makeFooBar();
```

###### ANSWER:
These code will return error because `makeBar()` has private access and cannot be called from `makeFoo()`

---

#### 2. You and your colleague work on the same codebase. Assume you always indent your code with four spacebars, but you started noticing he is pushing code formatting using tabs. You tried to convince him that spacebars are better than tabs, but he didn’t listen . What should you do?

###### ANSWER:
It depends on what language that we work together.

If it's JS then we could use standardize linter config (like using AirBnb code style) from the very beginning when the project just started. So, we can always maintain the consistency of our codebase.

Else, if it's on another language or the project is already in progress without some consistency rules applied before, then we will first discuss about how many indentation columns size that we will use on that codebase. It's because tab could have different number of indentation columns but space will always took one column, so tab or spaces doesn't matter if we already agree on the indentation size.

---

#### 3. Name the OOP principle which allows the function that takes a parameter of [class] type A and calls some of its methods, to behave differently depending on the argument's concrete type.

###### ANSWER:
Is it called polymorphism? Or method overload? I'm not very sure about this one.

---

#### 4. Is a statement like `require_once $_GET['filename'].'.php';` secure, why?

###### ANSWER:
I think it's not secure. As far as I know, `$_GET` is useful to get the value of query string, which the value is dynamic most of the time. If we use `require_once()` with `$_GET`, everyone can change the query string value at anytime (where I assume this app is a web app) and our app will then include the wrong file – even a remote file from outside of our server. It will lead us to a new security breach.

---

#### 5. In which cases this will trigger an error, and in which cases it won’t?
```php
function foo(int $i) :void{}
foo('1');
```

###### ANSWER:
These code will work when the argument is string, integer, float and boolean type; and will not work when the argument is not primitive, like array, object, null, etc.

---

#### 6. Consider you have two tables in MySQL database: `site` and `user`. `site` has the following labels `id`, `name`, `user_id` and `user` has the labels `id` and `login`. Write a query to select IDs from sites which owners have logins starting with "badguy".

###### ANSWER:
```mysql
mysql> select s.id from site s, user u where s.user_id = u.id and u.login = "badguy";
```

---

#### 7. You are working on a local git repository, which is cloned from the remote one (it is named "origin" on your local repo). It has the branches "master" and "v1.1.5". You are now on branch "master", with no changed files. You want to create a new branch "issue-1234" on top of the branch "v1.1.5". Please, create the file "feature-todo.txt" containing "// TODO" and publish the file on this (issue-1234) branch on the remote repo. Please write the commands (executable in Bash Linux shell) which will do this.

###### ANSWER:
```bash
$ git checkout v1.1.5
$ git checkout -b issue-1234
$ echo -e "// TODO" >> feature-todo.txt
$ git add . && git commit -m "Add feature todo list"
$ git push origin issue-1234
```

Origin is here -> <a href="https://github.com/arviantodwi/freelancer-phpjs-expert" target="_blank">freelancer-phpjs-expert</a>

---

#### 8. Why would you encapsulate data or behavior inside classes?

###### ANSWER:
I think the main purpose of encapsulation is to protect one or many things (in terms of properties and methods) inside an object, so the other objects will never be able to access those protected things.

---

#### 9. How would you robustly guarantee that the existing code containing some business logic won't behave wrongly after changes?

###### ANSWER:
- Implement the basic principle of functional programming whenever possible, only process the data for a single output based on the given input.
- Keep names of variables, functions, methods etc. clear enough to read.
- Test the existing code after changes. If test is not available, write some test first and make sure it's passed before write the changes.
- Write changes and refactor only for parts that need to be changed.

---

#### 10. Is it correct that the more comments easier to understand the code?

###### ANSWER:
No. I can say that we should never put a comment about what not to comment on. Comment is helpful but full of comments will confuse us more. Even more, too much comments will reduce readability of our code.

---

#### 11. Do you have any knowledge/experience related to PHP Frameworks? If you do, please tell me about it.

###### ANSWER:
Yes, I do have some experience with Laravel, Lumen, Yii and CodeIgniter. I also have tried Slim once but only for a proof of concept. Although I have some experience with those frameworks, I rarely use it on regular basis.
- I use Lumen in 2019 for backend API in my thesis,
- Laravel and Yii between 2015-2018 for few projects in my former company, and
- CodeIgniter in 2017 when I took software developer associate certification.

---

#### 12. There is an array consisting of numbers 7, 15, 17, 21, please write a simple PHP/Python (preferably both) script that will show the sum of all the values (output should be 60). Write the PHP script using a loop and without `array_sum`.

###### ANSWER:
I have no experience with Python but I quickly learn it for this test.
```php
# PHP
<?php
function my_array_sum (array $numbers) : int {
    $sum = 0;
    for ($i = 0; $i < count($numbers); $i += 1) {
        if (!is_int ($numbers[$i])) {
            print ("Array contains element that is not integer\n");
            return 0;
        }
        $sum += $numbers[$i];
    }

    return $sum;
}

printf ("%d\n", my_array_sum ([7, 15, 17, 21]));
```
```python
# Python
def my_array_sum (numbers):
    sum = 0
    for i in range (len (numbers)):
        if type (numbers[i]) != int:
            print ("Array contains element that is not integer")
            return
        sum += numbers[i]
    return sum

print (my_array_sum ([7, 15, 17, 21]))
```

---

#### 13. Please write a JS function called `makespace` that if called like this `makespace('something')` will make spaces between letters and print out 's o m e t h i n g' on the screen in alert box with 3 sec delay.

###### ANSWER:
```js
function makespace (str) {
    setTimeout(() => {
        const str_arr = str.split ("");
        const spaced_str = str_arr.reduce ((acc, char) => {
            return (acc == "")
                ? acc.concat (char)
                : acc.concat (" ".concat (char));
        }, "");
        alert (spaced_str);
    }, 3000);
}

makespace('something');
```

---

#### 14. Please write a script in PHP that will find the longest common part of two given strings. If there is more than one, please write all longest common parts. For example, when the script is given these two arguments: "Doors" "Kangaroo", it prompts "oo" as the longest common part.

###### ANSWER:
```php
<?php
function longest_common_substring (string $str1, string $str2, array $parts = [], int $cursor = 0) {
    if (strlen ($str1) <= 1 || strlen ($str2) === 0) {
        return $parts;
    }

    $needle = substr ($str1, 0, $cursor + 1);
    if (strpos ($str2, $needle) !== false) {
        if ($needle == $str1) {
            array_push ($parts, $needle);
            return longest_common_substring (substr ($str1, strlen ($needle)), $str2, $parts, 0);
        }
        return longest_common_substring ($str1, $str2, $parts, ++$cursor);
    } else if (strpos ($str2, $needle) === false && $cursor > 1) {
        $needle = substr ($needle, 0, -1);
        array_push ($parts, $needle);
        return longest_common_substring (substr ($str1, strlen ($needle)), $str2, $parts, 0);
    }

    return longest_common_substring (substr ($str1, 1), $str2, $parts, 0);
}

// "oo"
printf ("\"%s\"\n", implode (", ", longest_common_substring ("Doors", "Kangaroo")));
// "Kayak"
printf ("\"%s\"\n", implode (", ", longest_common_substring ("Kayak", "Kayak")));
// ""
printf ("\"%s\"\n", implode (", ", longest_common_substring ("Empty", "")));
// "_long, _string_for_longest_common_, string"
printf ("\"%s\"\n", implode (", ", longest_common_substring ("this_is_a_really_long_string_for_longest_common_substring", "_string_for_longest_common_")));
```
